# AGENTS.md - Skills IA Manager

Coding guidelines for AI agents working on this VSCode extension.

## Build Commands

```bash
npm run check-types   # Type checking only
npm run compile       # Compile TypeScript to JavaScript
npm run package       # Build for production
npm run watch         # Development with watch mode
npm run vscode:prepublish  # Prepare for publishing
```

## Testing
⚠️ **No testing framework configured.** When adding tests:
- Jest or Mocha for unit tests, `@vscode/test-electron` for VSCode testing
- Run single test: `npm test -- --testNamePattern="specific test"`

## File Structure
```
src/
├── services/          # Business logic (GitService, SkillScanner)
├── utils/            # Pure utilities (fs, ide, yaml, skills)
├── extension.ts      # Main entry, commands, UI
├── skillsProvider.ts # TreeView provider
├── configManager.ts  # Configuration handling
└── types.ts          # TypeScript interfaces/enums
```

## Import Order
```typescript
// 1. Node.js built-ins
import * as vscode from 'vscode';
import * as path from 'path';
import * as fs from 'fs';

// 2. Third-party libraries
import AdmZip = require('adm-zip');

// 3. Internal modules
import { SkillsProvider } from './skillsProvider';
import { Skill, SkillRepo } from './types';
```

## Naming Conventions
- **Variables/functions**: `camelCase` (`skillsTreeView`, `getRemoteBranches`)
- **Classes**: `PascalCase` (`GitService`, `SkillsProvider`)
- **Constants**: `SCREAMING_SNAKE_CASE` (`CACHE_DIR`, `DEFAULT_BRANCH`)
- **Files**: `camelCase` (`skillsProvider.ts`)
- **Boolean prefixes**: `isValidGitRepo`, `hasConflicts`

## TypeScript Patterns
```typescript
export enum SkillMatchStatus {
    NotInstalled = 'not_installed',
    Matched = 'matched',
    Conflict = 'conflict',
}

export interface Skill {
    name: string;
    repoUrl: string;
    localPath?: string;
    installed?: boolean;
}

function isSkillRepo(node: TreeNode): node is SkillRepo {
    return 'url' in node && !('type' in node);
}
```

## Error Handling
```typescript
// Async with throw
try {
    const result = await GitService.cloneRepo(url);
    return result;
} catch (error) {
    console.error(`Failed to clone ${url}:`, error);
    throw new Error(`Clone failed: ${error.message}`);
}

// VSCode user-facing
try {
    await vscode.workspace.fs.writeFile(uri, content);
} catch (error) {
    vscode.window.showErrorMessage(`Failed: ${error.message}`);
}

// Network with retry
for (let attempt = 1; attempt <= 3; attempt++) {
    try {
        return await fetchRemoteSkills(url);
    } catch (e) {
        if (attempt < 3) await sleep(attempt === 1 ? 200 : 500);
    }
}
```

## VSCode Extension Patterns
```typescript
// Console logging via outputChannel
const outputChannel = vscode.window.createOutputChannel('Agent Skills Manager');
context.subscriptions.push(outputChannel);
const originalLog = console.log;
console.log = (...args: any[]) => {
    outputChannel.appendLine(`[INFO] ${args.join(' ')}`);
    originalLog.apply(console, args);
};

// Command registration
context.subscriptions.push(
    vscode.commands.registerCommand('agentskills.refresh', () => skillsProvider.refresh())
);

// TreeView with drag & drop
const treeView = vscode.window.createTreeView('agentskills-skills', {
    treeDataProvider,
    canSelectMany: true,
    dragAndDropController: {
        dragMimeTypes: ['application/vnd.agentskills.node'],
        dropMimeTypes: ['application/vnd.agentskills.node'],
        handleDrag: (source, dataTransfer) => {
            dataTransfer.set(mimeType, new vscode.DataTransferItem(JSON.stringify({...})));
        },
        handleDrop: (target, dataTransfer) => { /* ... */ }
    }
});
context.subscriptions.push(treeView);

// Configuration access
const config = vscode.workspace.getConfiguration('agentSkills');
const repos = config.get<SkillRepo[]>('repositories', []);
```

## Performance & Common Pitfalls
- Use `Map<string, Skill[]>` for O(1) lookups
- Cache expensive operations (git, file I/O)
- Use `vscode.workspace.fs` for async file operations
- Always dispose: `context.subscriptions.push(disposable)`
- **Don't** use `console.log` directly - use outputChannel
- **Don't** forget to add disposables to `context.subscriptions`
- **Don't** block UI with sync file operations
- **Don't** ignore TypeScript strict mode warnings
- **Do** handle network failures with retries
- **Do** use `vscode.window.showErrorMessage` for user errors

## Multi-IDE Support
- Use `detectIde(process.env, vscode.env.appName)` from `utils/ide`
- Skills dirs vary: `.claude/skills`, `.cursor/rules`, etc.
- Use `getProjectSkillsDir(workspaceRoot, ide)` for correct path
