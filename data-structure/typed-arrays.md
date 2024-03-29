## 数据结构：类型数组

数组是一种 JavaScript 对象，它能存储各种数据类型的元素。

```
var complexArr = [1, 5, "2", "Word", {"name": "James"}];
```

通常浏览器会自动地为数组分配合适的内存空间，同时内存大小也会随着你增删元素而发生变化。

然而，在一些对性能有较高要求以及存在不同数据类型的场景下，我们需要更精确地给数组分配内存空间。

Typed arrays就是解决这类问题的一种方案。我们可以精确地给一个数组分配内存空间。下面的表格列出了这种数组能够存放的数据类型以及不同数据类型所占据的字节数。

| 类型                | 元素所占字节数 |
| :------------------ | :------------- |
| `Int8Array`         | 1              |
| `Uint8Array`        | 1              |
| `Uint8ClampedArray` | 1              |
| `Int16Array`        | 2              |
| `Uint16Array`       | 2              |
| `Int32Array`        | 4              |
| `Uint32Array`       | 4              |
| `Float32Array`      | 4              |
| `Float64Array`      | 8              |

创建这类数组有两种方式，一种是直接创建，如下代码创建了一个长度为 3 的 `Int16Array`：

> var i8 = new Int16Array(3);
> console.log(i8);
> // 输出 [0, 0, 0]

我们也可以通过创建buffer的方式来决定一个数组要容纳多少元素（以 bytes 为单位）。

**注意：**
使用`ArrayBuffer`创建`Typed array`时，我们需要传入一个表示`ArrayBuffer`大小的数字。由于其单位为字节，因此它必须是偶数：

> // 用另一种方式创建和上面相同的 Int16Array
> var byteSize = 6; // 必须是 2 的倍数
> var buffer = new ArrayBuffer(byteSize);
> var i8View = new Int16Array(buffer);
> buffer.byteLength; // 输出 6
> i8View.byteLength; // 输出 6
> console.log(i8View); // 输出 [0, 0, 0]

Buffers是存放数据的通用对象，你无法直接访问它们。若要访问它们。你需要先创建一个 view。

> i8View[0] = 42;
> console.log(i8View); // 输出 [42, 0, 0]

**注意：**
Typed Arrays 没有`.pop()`或`.push()`这些传统数组拥有的方法。使用`Array.isArray()`方法对 Typed Arrays 做判断返回的是`false`，而非`true`。因为 Typed Arrays 的接口相对简洁，因此对 JavaScript 引擎来说，实现这类数组会更加容易。



```
var buffer = new ArrayBuffer(64);
var i32View = new Int32Array(buffer);
console.log(i32View.length)
```



------



请先创建一个 64 个字节的`buffer`，再创建一个类型是`Int32Array`名称叫做`i32View`的视图。

运行测试重置代码[获取提示](https://guide.freecodecamp.org/certifications/coding-interview-prep/data-structures/typed-arrays)请求帮助



------

# JavaScript 类数组对象


  MDN文档：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays

JavaScript类型化数组是一种类似数组的对象，并提供了一种用于访问原始二进制数据的机制。 正如你可能已经知道，[`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array) 存储的对象能动态增多和减少，并且可以存储任何JavaScript值。JavaScript引擎会做一些内部优化，以便对数组的操作可以很快。然而，随着Web应用程序变得越来越强大，尤其一些新增加的功能例如：音频视频编辑，访问WebSockets的原始数据等，很明显有些时候如果使用JavaScript代码可以快速方便地通过类型化数组来操作原始的二进制数据将会非常有帮助。

但是，不要把类型化数组与正常数组混淆，因为在类型数组上调用  [`Array.isArray()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)  会返回`false`。此外，并不是所有可用于正常数组的方法都能被类型化数组所支持（如 push 和 pop）。

## 缓冲和视图：类型数组架构[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#缓冲和视图：类型数组架构)

为了达到最大的灵活性和效率，JavaScript 类型数组（[Typed Arrays](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays)）将实现拆分为**缓冲**和**视图**两部分。一个缓冲（由 [`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 对象实现）描述的是一个数据块。缓冲没有格式可言，并且不提供机制访问其内容。为了访问在缓冲对象中包含的内存，你需要使用视图。视图提供了上下文 — 即数据类型、起始偏移量和元素数 — 将数据转换为实际有类型的数组。

![Typed arrays in an ArrayBuffer](https://mdn.mozillademos.org/files/8629/typed_arrays.png)

### ArrayBuffer[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#ArrayBuffer)

 [`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 是一种数据类型，用来表示一个通用的、固定长度的二进制数据缓冲区。你不能直接操纵一个ArrayBuffer中的内容；你需要创建一个类型化数组的视图或一个描述缓冲数据格式的[`DataView`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/DataView)，使用它们来读写缓冲区中的内容.

### 类型数组视图[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#类型数组视图)

类型化数组视图具有自描述性的名字和所有常用的数值类型像`Int8`，`Uint32`，`Float64` 等等。有一种特殊类型的数组`Uint8ClampedArray`。它仅操作0到255之间的数值。例如，这对于[Canvas数据处理](https://developer.mozilla.org/zh-CN/docs/Web/API/ImageData)非常有用。

| Type                                                         | Value Range               | Size in bytes | Description                                                  | Web IDL type          | Equivalent C type               |
| ------------------------------------------------------------ | ------------------------- | ------------- | ------------------------------------------------------------ | --------------------- | ------------------------------- |
| [`Int8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int8Array) | -128 to 127               | 1             | 8-bit two's complement signed integer                        | `byte`                | `int8_t`                        |
| [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) | 0 to 255                  | 1             | 8-bit unsigned integer                                       | `octet`               | `uint8_t`                       |
| [`Uint8ClampedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray) | 0 to 255                  | 1             | 8-bit unsigned integer (clamped)                             | `octet`               | `uint8_t`                       |
| [`Int16Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int16Array) | -32768 to 32767           | 2             | 16-bit two's complement signed integer                       | `short`               | `int16_t`                       |
| [`Uint16Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint16Array) | 0 to 65535                | 2             | 16-bit unsigned integer                                      | `unsigned short`      | `uint16_t`                      |
| [`Int32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array) | -2147483648 to 2147483647 | 4             | 32-bit two's complement signed integer                       | `long`                | `int32_t`                       |
| [`Uint32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint32Array) | 0 to 4294967295           | 4             | 32-bit unsigned integer                                      | `unsigned long`       | `uint32_t`                      |
| [`Float32Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array) | 1.2x10-38 to 3.4x1038     | 4             | 32-bit IEEE floating point number ( 7 significant digits e.g. 1.1234567) | `unrestricted float`  | `float`                         |
| [`Float64Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array) | 5.0x10-324 to 1.8x10308   | 8             | 64-bit IEEE floating point number (16 significant digits e.g. 1.123...15) | `unrestricted double` | `double`                        |
| [`BigInt64Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt64Array) | -263 to 263-1             | 8             | 64-bit two's complement signed integer                       | `bigint`              | `int64_t (signed long long)`    |
| [`BigUint64Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigUint64Array) | 0 to 264-1                | 8             | 64-bit unsigned integer                                      | `bigint`              | `uint64_t (unsigned long long)` |

### 数据视图[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#数据视图)

[`DataView`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/DataView) 是一种底层接口，它提供有可以操作缓冲区中任意数据的读写接口。这对操作不同类型数据的场景很有帮助，例如：类型化数组视图都是运行在本地字节序模式(参考 [Endianness](https://developer.mozilla.org/en-US/docs/Glossary/Endianness))，可以通过使用 `DataView `来控制字节序。默认是大端字节序(Big-endian)，但可以调用读写接口改为小端字节序(Little-endian)。

## 使用类型数组的Web API[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#使用类型数组的Web_API)

- [`FileReader.prototype.readAsArrayBuffer()`](https://developer.mozilla.org/en-US/docs/Web/API/FileReader#readAsArrayBuffer())

  `FileReader.prototype.readAsArrayBuffer()` 读取对应的[`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) 或 [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File)的内容

- [`XMLHttpRequest.prototype.send()`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest#send())

  `XMLHttpRequest` 实例的 `send()` 方法现在使用支持类型化数组和 [`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 对象作为参数。

- `ImageData.data`

  是一个 [`Uint8ClampedArray`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray) 对象，用来描述包含按照RGBA序列的颜色数据的一维数组，其值的范围在`0`到`255`（包含255）之间。

## 示例[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#示例)

### 使用视图和缓冲[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#使用视图和缓冲)

首先，我们创建一个16字节固定长度的缓冲：

```
var buffer = new ArrayBuffer(16);
```

现在我们有了一段初始化为0的内存，目前还做不了什么太多操作。让我们确认一下数据的字节长度：

```js
if (buffer.byteLength === 16) {
  console.log("Yes, it's 16 bytes.");
} else {
  console.log("Oh no, it's the wrong size!");
}
```

在实际开始操作这个缓冲之前，需要创建一个视图。我们将创建一个视图，此视图将把缓冲内的数据格式化为一个32位的有符号整数数组：

```
var int32View = new Int32Array(buffer);
```

现在我们可以像普通数组一样访问该数组中的元素：

```js
for (var i = 0; i < int32View.length; i++) {
  int32View[i] = i * 2;
}
```

该代码会将数组以0, 2, 4和6填充 （一共4个4字节元素，所以总长度为16字节）。

### 同一数据的多个视图[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#同一数据的多个视图)

更有意思的是，你可以在同一数据上创建多个视图。例如：基于上文的代码，我们可以添加如下代码处理：

```js
var int16View = new Int16Array(buffer);

for (var i = 0; i < int16View.length; i++) {
  console.log("Entry " + i + ": " + int16View[i]);
}
```

这里我们创建了一个2字节整数视图，该视图共享上文的4字节整数视图的缓冲，然后以2字节整数打印出缓冲里的数据，这次我们会得到0, 0, 2, 0, 4, 0, 6, 0这样的输出。

那么，这样呢？

```js
int16View[0] = 32;
console.log("Entry 0 in the 32-bit array is now " + int32View[0]);
```

这次的输出是"Entry 0 in the 32-bit array is now 32"。也就是，这2个数组都是同一数据的以不同格式展示出来的视图。你可以使用任何一种 [view types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray#TypedArray_objects) 中的定义的视图。

### 使用复杂的数据结构[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#使用复杂的数据结构)

通过将缓冲与不同类型视图组合，以及修改内存访问的偏移位置，你可以操作包含更多更复杂数据结构的数据。你可以使用[js-ctypes](https://developer.mozilla.org/en-US/docs/Mozilla/js-ctypes)操作诸如[WebGL](https://developer.mozilla.org/en-US/docs/Web/WebGL)，数据文件或C语言结构体这些复杂的数据结构。

请看如下的C语言结构:

```cpp
struct someStruct {
  unsigned long id;
  char username[16];
  float amountDue;
};
```

你可以采用如下代码访问一个包含此类结构体的缓冲：

```js
var buffer = new ArrayBuffer(24);

// ... read the data into the buffer ...

var idView = new Uint32Array(buffer, 0, 1);
var usernameView = new Uint8Array(buffer, 4, 16);
var amountDueView = new Float32Array(buffer, 20, 1);
```

现在你就可以通过`amountDueView[0]`的方式访问数量。

**提示：**C语言结构体的[数据对齐](http://en.wikipedia.org/wiki/Data_structure_alignment)与平台相关。因此需要防范和考虑不同平台的字节填充对齐。

### 转换为普通数组[节](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Typed_arrays#转换为普通数组)

在处理完一个类型化数组后，有时需要把它转为普通数组，以便可以可以像普通数据一种操作访问。可以调用 [`Array.from`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)实现这种转换，如果 `Array.from` 不支持的话，也可以通过如下代码实现：

```js
var typedArray = new Uint8Array([1, 2, 3, 4]),
    normalArray = Array.prototype.slice.call(typedArray);
normalArray.length === 4;
normalArray.constructor === Array;
```