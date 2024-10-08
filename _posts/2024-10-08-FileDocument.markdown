---
layout: post
title: "FileDocument VS ReferenceFileDocument in Swift"
---

In SwiftUI, `FileDocument` and `ReferenceFileDocument` are protocols used to represent and manage different types of files within a document-based application. Both have specific use cases depending on how the file is loaded, managed, and manipulated in memory. Here's an explanation of each and when to use them:

### 1. `FileDocument`

**Use Case: In-Memory File Handling**

`FileDocument` is used when you want to load a file completely into memory, manipulate it, and then potentially save it back to disk. This is ideal for smaller files that can be loaded into memory without performance issues. When a file is loaded into memory, the entire content of the file is available, allowing you to work with it directly.

#### Key Characteristics

- Suitable for smaller files that fit in memory.
- Entire file is read into memory, which is then manipulated.
- You can use Swift's in-memory structures like `Data` or `String` for file content.
- Good for document formats like text, images, audio, etc.

#### Example of `FileDocument`

Here's an example of a simple `FileDocument` for handling a text file:

```swift
import SwiftUI
import UniformTypeIdentifiers

struct TextDocument: FileDocument {
    static var readableContentTypes = [UTType.plainText]
    var text: String = ""

    init(initialText: String = "") {
        self.text = initialText
    }

    init(configuration: ReadConfiguration) throws {
        guard let data = configuration.file.regularFileContents,
              let string = String(data: data, encoding: .utf8) else {
            throw CocoaError(.fileReadCorruptFile)
        }
        text = string
    }

    func fileWrapper(configuration: WriteConfiguration) throws -> FileWrapper {
        let data = text.data(using: .utf8)!
        return FileWrapper(regularFileWithContents: data)
    }
}
```

#### Use Cases

- **Text Editing:** For editing small to medium-sized text files (like Markdown, plaintext, etc.), where the entire content needs to be read into memory for easy manipulation.
- **Image Files:** If you're working with image files, where you load the image, allow users to edit it, and then save the modified image back to disk.
- **Audio Files:** For handling small audio files where the entire file is loaded into memory and manipulated (cut, processed, etc.).

### 2. `ReferenceFileDocument`

**Use Case: Large File Handling with On-Demand Access**

`ReferenceFileDocument` is used for large files where loading the entire content into memory isn't feasible or efficient. Instead of reading the entire file, this protocol allows you to reference the file and operate on it directly from disk, making it more suitable for large files like videos, databases, or large datasets.

#### Key Characteristics

- Suitable for large files that cannot be loaded entirely into memory.
- File access is performed by referencing the file on disk, allowing for partial reads or modifications.
- Works well for scenarios like video editing, audio editing, or other large multimedia/document handling tasks.
- You generally perform on-demand or incremental file access.

#### Example of `ReferenceFileDocument`

Here’s an example of how you might implement `ReferenceFileDocument` for handling large video files:

```swift
import SwiftUI
import UniformTypeIdentifiers

struct VideoDocument: ReferenceFileDocument {
    static var readableContentTypes = [UTType.movie]
    var fileURL: URL
    
    init(fileURL: URL) {
        self.fileURL = fileURL
    }
    
    init(configuration: ReadConfiguration) throws {
        fileURL = configuration.file.fileURL!
    }

    func snapshot(contentType: UTType) throws -> URL {
        return fileURL
    }

    func fileWrapper(snapshot: URL, configuration: WriteConfiguration) throws -> FileWrapper {
        return try FileWrapper(url: snapshot)
    }
}
```

#### Use Cases

- **Video Editing:** When you're working with large video files, and reading the entire video into memory isn't practical. Instead, you reference the file on disk and manipulate specific portions of it (e.g., trimming video).
- **Large Data Sets:** If you're working with scientific data or large datasets, where you only need access to specific sections of a file on-demand.
- **Database Files:** When working with large databases or structured files where you might want to query or modify specific records without loading the entire file into memory.

### Summary of Use Cases

| Protocol              | Use Cases                                     | Characteristics |
|-----------------------|-----------------------------------------------|-----------------|
| `FileDocument`         | Small to medium files (e.g., text, images)    | Loads the entire file into memory, suitable for small to medium files. |
| `ReferenceFileDocument`| Large files (e.g., videos, large datasets)    | Operates directly from the file on disk, suitable for large files that can't fit in memory. |

Both protocols help in managing documents in SwiftUI, but `FileDocument` is preferable when you're working with files that can comfortably fit into memory, while `ReferenceFileDocument` is better for handling large files that require partial or on-demand access to avoid memory overuse.
