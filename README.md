# music-ai

Non-official [Music AI](https://music.ai/docs/getting-started/introduction/) (Before called Moises AI) API wrapper package with Typescript support

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/3e0b2e2d5b9d4157a26d7faebe3f5a6f)](https://app.codacy.com/gh/leandrosimoes/moises/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)


## Install

`yarn add @lesimoes.dev/music-ai`

or

`npm i @lesimoes.dev/music-ai`

## How to use it?

```typescript
// importing into your project
import { 
    processFile, 
    processFolder, 
    ProcessStatus, 
    ProcessFileOptions,
    JobStatus,
    DownloadResult
} from '@lesimoes.dev/music-ai'

// types exported by the library
export type ProcessStatus =
    | 'PENDING'
    | 'PROCESSING'
    | 'SUCCEEDED'
    | 'FAILED'
    | 'ABORTED'

export type ProcessFolderOptions = {
    apiKey: string
    workflowId: string
    inputFolder: string
    outputFolder: string
    maxConcurrencyNumber?: number
    abortSignal?: AbortSignal
    jobMonitorInterval?: number
    onProgress?: (
        file: string,
        status: JobStatus | ProcessStatus,
        report: any
    ) => Promise<void>
    onLog?(message: string): Promise<void>
    onError?(message: string): Promise<void>
}

export type ProcessFileOptions = {
    apiKey: string
    workflowId: string
    filePath: string
    outputFolder: string
    jobMonitorInterval?: number
    onProgress?: (
        file: string,
        status: JobStatus | ProcessStatus,
        report: any
    ) => Promise<void>
    onLog?(message: string): Promise<void>
    onError?(message: string): Promise<void>
}

export type JobStatus =
    | 'SUCCEEDED'
    | 'FAILED'
    | 'PENDING'
    | 'PROCESSING'
    | 'DELETED'
    | 'QUEUED'
    | 'CANCELLED'
    | 'STARTED'

export type DownloadResult = {
    [key: string]: string
}

// functions exported by the library
async function processFile({
    apiKey,
    workflowId,
    filePath,
    outputFolder,
    jobMonitorInterval,
    onProgress,
    onLog,
    onError,
}: ProcessFileOptions) : Promise<DownloadResult>

async function processFolder({
    apiKey,
    workflowId,
    inputFolder,
    outputFolder,
    maxConcurrencyNumber = 5,
    abortSignal,
    jobMonitorInterval = 1000,
    onProgress,
    onLog,
    onError,
}: ProcessFolderOptions): Promise<DownloadResult[]>
```