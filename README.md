# Size parameter extension

From: Marek Küthe (m.k@mk16.de)
Last updated: 29.08.2022


## 1. Overview

### 1.1 Motivation

The Gemini protocol can be used to deliver files. In contrast to Gopher, there is no line with a dot to indicate the end of a transfer. Therefore, it can happen that only parts of large files are transferred. This can happen especially with unstable or slow connections. One way to prevent this is to pass the length of the content as meta information to the client.

## 2. Extension

When a file is successfully delivered from a Gemini server, it returns a 2x status code. The meta information returned is the mimetype with some other parameters. These parameters are currently described in paragraph 3.3 and 5.2 of the Gemini specification.

This extension introduces the new parameter `size`. This specifies the length in bytes of the file that will be delivered.

## 2.1 Client support

This extension is optional and not mandatory. Gemini clients that do not support this extension can ignore the parameter. Thus, it is possible that a server supports the extension, but the client does not.

Note: A test with the popular Lagrange client showed that it simply ignores unknown parameters.

## 2.2 Long life connections

It can happen that you want to open a page with the Gemini protocol as a kind of stream. The server keeps the connection open and sends new data sporadically. The client should not close the connection. In this case the parameter `size` can be set to a negative number, typically `-1`.

## 3. Example

A client requests a file from server:

```
gemini://gemini.example.com/mybib.bin
```

The server responds and specifies the size of the file:

```
20 application/octet-stream; size=1073741824
<... some binary data ...>
```

## 4. See also

gemini://twins.rocketnine.space/proposals.gmi
