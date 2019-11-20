### 1、IO流的基本图

![1574237735247](C:\Users\huangqianhong\AppData\Roaming\Typora\typora-user-images\1574237735247.png)

这里要感谢[帅果果的博客](https://www.cnblogs.com/shuaiguoguo/p/8883862.html)

~~自己画的图导出来有水印，不想破解，就尴尬的盗一下，帅果果大佬，要是觉得侵权，可以联系我，小菜鸡瑟瑟发抖呢~~



## 2、Io流的简介

IO流是相对的的表现形式，我们一般是以java程序和文本来打比方，当我们程序想要获取的文本数据的时候，我们可以使用输入流（InputStream或者是writer）,反之，我们使用输出流（OutputStream或者是Reader）.

### 2、1字符流和字节流的区别

数据存储在硬盘都是以二进制的形式进行存储，而通过字节流（InputStream和OutputStream）可以读取任意文件，字符流只能存取纯文本数据（当他读到一个字节的时候，去查找指定的编码表，返回对应的编码）。

所以，面对纯文本数据，我们优先使用字符流（Writer和Reader）,其他的情况使用字节流（InputStream和OutputStream）.

### 2、2字符流

1）字节输入流

> FileInputStream(String name);	//通过FileInputStream打开一个连接，这个参数是在文件系统的路径
>
> FileInputStream(File file);		//通过FileInputStream打开一个连接，这个参数是文件系统的文件
>
> BufferedInputStream（FileInputStream in）	//创建一个输入流BufferedInputStream,
>
> BufferedInputStream（FileInputStream in,int size) //创建一个输出流bufferedinputStream,有一定的大小



2）字符输入流

> BufferReader(Reader in);     //
>
> BufferedReader(Reader in, int sz）
>
> BufferedWriter(Writer in, int sz）
>
> 



```java
	//这个是利用FileInputStream创建的
	public static void read() {
		File file = new File("E:"+File.separator+"Desktop"+File.separator+"1.txt");
		try {
			FileInputStream inputStream = new FileInputStream(file);
			byte[] bs = new byte[1024];
			StringBuffer buffer = new StringBuffer("");
			while(inputStream.read(bs)!=-1) {
				buffer.append(new String(bs));		//因为他是字符数组，所以如果直接添加的话，
													//可能添加的是字符数组的首地址
			}
			System.out.println(buffer.toString());
			inputStream.close();
		} catch (FileNotFoundException e) {
			
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
```

```java
//BufferedInputStream bInputStream = new BuufferedInputStream(new FileInputStream(File file));
public static void readBuffer() {
		File file = new File("E:"+File.separator+"Desktop"+File.separator+"2.xlsx");	//这个是你自己的文件路径，你可以自己设置
		File file2 = new File("E:"+File.separator+"Desktop"+File.separator+"3.xlsx");	//File.separator是为了跨平台使用的
		
		try {
			BufferedInputStream bInputStream = new BufferedInputStream(new FileInputStream(file));
			BufferedOutputStream bOutputStream = new BufferedOutputStream(new FileOutputStream(file2));
			int len = 0;
			byte[] bs = new byte[1024];
			while((len = bInputStream.read(bs)) !=-1) {
				bOutputStream.write(bs);
//				bOutputStream.write(bs, 0, len);
			}
			bOutputStream.close();
			bInputStream.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
```

~~这里开始字符流的代码了,因为用的比较少啊，我就写一个代码了哈，剩下的你们自己补补~~

```java
public static void InputReader() {
		File file = new File("E:"+File.separator+"Desktop"+File.separator+"2.xlsx");
		try {
			BufferedReader in = new BufferedReader(new FileReader(file));//使用本地环境中的默认字符集，例如在中文环境中将使用 GBK编码
			String line = null;
			while((line = in.readLine()) != null){
				System.out.println(line);
			}
			in.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
		
	}
```

