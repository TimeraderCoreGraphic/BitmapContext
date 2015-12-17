# BitmapContext
###BitmapContext二三事
BitmapContext使用还是比较简单的。

###内存释放的回调方法。
	typedef void (*CGBitmapContextReleaseDataCallback)(void * __nullable releaseInfo,
    void * __nullable data);
###创建以及参数。
创建有两个方法，其中一个相当于另外一个的扩张。没有很大的出入。  

	CG_EXTERN CGContextRef __nullable CGBitmapContextCreateWithData(
    void * __nullable data, size_t width, size_t height, size_t bitsPerComponent,	size_t bytesPerRow, CGColorSpaceRef __nullable space, uint32_t bitmapInfo,
	CGBitmapContextReleaseDataCallback __nullable releaseCallback,
	void * __nullable releaseInfo)CG_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_4_0);
	/*---------------------------------------------------------*/  
	CG_EXTERN CGContextRef __nullable CGBitmapContextCreate(void * __nullable data,
    size_t width, size_t height, size_t bitsPerComponent, size_t bytesPerRow,
    CGColorSpaceRef __nullable space, uint32_t bitmapInfo)
    CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
1. data:传入一些数据，在释放的回调方法可以获得，也可以用：  

		CG_EXTERN void * __nullable CGBitmapContextGetData(CGContextRef __nullable context)
	    CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
2. width:像素宽度。
3. height:像素高度。
4. bitsPerComponent:内存中像素的每个组件的位数.例如，对于32位像素格式和RGB颜色空间，你应该将这个值设为8。
5. bitsPerRow:bitmap的每一行在内存所占的比特数  width * (bitsPerComponent * number of components + 7)/8。
6. space:bitmap上下文使用的颜色空间。
7. bitmapInfo:指定bitmap是否包含alpha通道，像素中alpha通道的相对位置（ARGB RGBA等），像素组件是整形还是浮点型等信息的字符串（存储的大小端啊）。
8. releaseCallback:释放的回调函数。
9. releaseInfo:释放时候回调带的info。
		
###各个参数数据获取。
各种Get方法。

###生成CGImageRef
	CG_EXTERN CGImageRef __nullable CGBitmapContextCreateImage(
    CGContextRef __nullable context)
    CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
