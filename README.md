# URLSessionHelper

`URLSessionHelper` is a Swift utility class that simplifies making HTTP network requests. It provides a convenient way to perform GET, POST, PUT, DELETE requests, and upload multipart data using the `URLSession` framework.

## Features

- **Singleton Pattern**: Ensures a single shared instance for consistent use throughout the app.
- **Convenient Methods**: Simplifies HTTP requests with easy-to-use methods.
- **Error Handling**: Provides meaningful error messages and response handling.
- **Multipart Data Upload**: Supports uploading files via multipart form data.

## Installation

### Manual Installation

1. Download the `URLSessionHelper.swift` file.
2. Add the file to your Xcode project.

## Usage

### Import Foundation

Make sure to import the `Foundation` framework:

```swift
import Foundation
let sessionHelper = URLSessionHelper.shared

GET Request
let url = URL(string: "https://jsonplaceholder.typicode.com/posts")!

sessionHelper.get(url) { result in
    switch result {
    case .success(let data):
        // Handle success - parse the data
        if let json = try? JSONSerialization.jsonObject(with: data, options: []) {
            print("GET Request Successful: \(json)")
        }
    case .failure(let error):
        // Handle failure
        print("GET Request Failed: \(error)")
    }
}

POST Request
let postUrl = URL(string: "https://jsonplaceholder.typicode.com/posts")!
let parameters: [String: Any] = [
    "title": "foo",
    "body": "bar",
    "userId": 1
]

sessionHelper.post(postUrl, parameters: parameters) { result in
    switch result {
    case .success(let data):
        // Handle success - parse the data
        if let json = try? JSONSerialization.jsonObject(with: data, options: []) {
            print("POST Request Successful: \(json)")
        }
    case .failure(let error):
        // Handle failure
        print("POST Request Failed: \(error)")
    }
}

PUT Request
let putUrl = URL(string: "https://jsonplaceholder.typicode.com/posts/1")!
let updateParameters: [String: Any] = [
    "id": 1,
    "title": "foo updated",
    "body": "bar updated",
    "userId": 1
]

sessionHelper.put(putUrl, parameters: updateParameters) { result in
    switch result {
    case .success(let data):
        // Handle success - parse the data
        if let json = try? JSONSerialization.jsonObject(with: data, options: []) {
            print("PUT Request Successful: \(json)")
        }
    case .failure(let error):
        // Handle failure
        print("PUT Request Failed: \(error)")
    }
}

DELETE Request
let deleteUrl = URL(string: "https://jsonplaceholder.typicode.com/posts/1")!

sessionHelper.delete(deleteUrl) { result in
    switch result {
    case .success(let data):
        // Handle success
        print("DELETE Request Successful")
    case .failure(let error):
        // Handle failure
        print("DELETE Request Failed: \(error)")
    }
}


Upload Multipart Data
let uploadUrl = URL(string: "https://yourapi.com/upload")!
let fileData = Data() // Replace with actual data to upload
let fileName = "example.txt"

sessionHelper.sendMultipartData(url: uploadUrl, data: fileData, fileName: fileName) { result in
    switch result {
    case .success(let data):
        // Handle success
        if let responseString = String(data: data, encoding: .utf8) {
            print("Upload Successful: \(responseString)")
        }
    case .failure(let error):
        // Handle failure
        print("Upload Failed: \(error)")
    }
}
