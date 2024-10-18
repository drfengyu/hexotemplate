- [TypeError: body used already for - should be able to extract twice ...](https://github.com/node-fetch/node-fetch/issues/533)
- [fetch body里数据为ReadableStream 解决办法 - winyh - 博客园](https://www.cnblogs.com/winyh/p/7053054.html)
- [(bug): Unable to read raw request body after hono 3.5.0](https://github.com/honojs/hono/issues/1387)
- [What does this error mean — Uncaught TypeError: Already read?](https://stackoverflow.com/questions/34786358/what-does-this-error-mean-uncaught-typeerror-already-read)
- [Reread a response body from JavaScript's fetch - Stack Overflow](https://stackoverflow.com/questions/40497859/reread-a-response-body-from-javascripts-fetch)

错误信息 **"Body has already been used. It can only be used once. Use tee() first if you need to read it twice."** 表明你正在尝试多次读取一个响应体（Response Body），而响应体只能读取一次。这是因为 Fetch API 的响应体是一个流（stream），一旦读取，就会被消耗，无法再次读取。

### 解决方法

1. **使用 `Response.clone()`**:
   - 你可以使用 `response.clone()` 创建响应的一个副本，然后分别从两个响应中读取内容。这样可以避免 "Body has already been used" 的错误。
   - 示例代码：
     ```javascript
     const response = await fetch(request);
     const responseClone = response.clone(); // 克隆响应

     const jsonData = await responseClone.json(); // 从克隆中读取 JSON
     const textData = await response.text(); // 从原始响应中读取文本
     ```

2. **使用 `Response.body.tee()`**:
   - `tee()` 方法可以将一个响应体流分成两个可读流。这样可以在一个流中读取内容，同时在另一个流中保留原始响应。
   - 示例代码：
     ```javascript
     const response = await fetch(request);
     const [stream1, stream2] = response.body.tee(); // 分割流

     const textData = await stream1.text(); // 从第一个流读取文本
     // 你可以使用 stream2 进行其他操作
     ```

3. **检查 `bodyUsed` 属性**:
   - 你可以通过检查 `response.bodyUsed` 属性来判断响应体是否已经被读取过。如果已经读取，可以选择不再读取，或者根据需要进行处理。
   - 示例代码：
     ```javascript
     if (!response.bodyUsed) {
         const textData = await response.text();
     } else {
         console.log("Response body has already been used.");
     }
     ```

### 结论

要避免 **"Body has already been used"** 的错误，最有效的方式是使用 `Response.clone()` 或 `Response.body.tee()` 方法来处理响应体。这些方法允许你在不消耗原始响应的情况下多次读取内容。如果你只需读取一次，确保在读取后不要再次尝试读取同一响应体。
