# NewPagedFlowView 1.1.5
###1.实现了什么功能
* 页面滚动的方向分为横向和纵向
* 目的:实现类似于选择电影票的效果,并且实现无限/自动轮播
* 特点:1.无限轮播;2.自动轮播;3.电影票样式的层次感;4.非当前显示view具有缩放和透明的特效

###2.版本信息
#####Version 1.1.5:

 * 首次不会自动滚动的bug
 * 解决scrollToPage 无法跳转到正确页面的bug

**具体含义请看源代码, 如发现bug请联系:799573715@qq.com (2016-08-12)**
***

#####Version 1.1.4:

 * 完美解决导航控制器出现的bug
 * 添加二级控制器
 * Main.storyboard添加导航控制器
 * 注意:
 	 * 1.使用导航控制器(UINavigationController)
     如果控制器中不存在UIScrollView或者继承自UIScrollView的UI控件
     请使用UIScrollView作为NewPagedFlowView的容器View,才会显示正常
     * 2.push出的二级页面,应在dealloc或者返回按钮里调用停止定时器方法
         [self.pageFlowView stopTimer];

**具体含义请看源代码, 如发现bug请联系:799573715@qq.com (2016-08-11)**
***

#####Version 1.1.2:

 * 处理一张图片时的展示问题
 * 处理一张图时的图片滚动bug
 * 非当前显示图片缩放更美观
 * 增加代理方法:- (void)didSelectCell:(UIView *)subView withSubViewIndex:(NSInteger)subIndex;(点击了第几个cell)

**具体含义请看源代码, 如发现bug请联系:799573715@qq.com (2016-08-08)**
***
#####Version 1.1.1:

 * 简化数组,使用时只需创建一个图片数组即可
 * 解决首次加载时,直接从第一页跳到第三页的bug
 * 解决拖动时,偶尔乱跳的bug
 * 指示Label更明确
 * 增加代理方法的介绍
 <br>
 **具体含义请看源代码, 如发现bug请联系:799573715@qq.com (2016-08-03)**
<br>
***

#####Version 1.0:
* 页面滚动的方向分为横向和纵向
* 目的:实现类似于选择电影票的效果,并且实现无限/自动轮播
 
* 特点:1.无限轮播;2.自动轮播;3.电影票样式的层次感;4.非当前显示view具有缩放和透明的特效

###3.动画效果
<img src="gif/NewPagedFlowViewGif.gif" width="100%">
</br>动图请移步:</br>
  <a href="http://example.com/">http://ww4.sinaimg.cn/mw690/9c6a8c79jw1f6geyiao4tg20a00dc4qu.gif</a>

###4.功能介绍
	/**
	 *  开启定时器
	*/
	- (void)startTimer;

	/**
	 *  关闭定时器
	 */
	- (void)stopTimer;
	
	
**代理方法的使用**

    @protocol  NewPagedFlowViewDelegate<NSObject>

	/**
	 *  单个子控件的Size
	 *
	 *  @param flowView <#flowView description#>
	 *
	 *  @return <#return value description#>
	*/
	- (CGSize)sizeForPageInFlowView:(NewPagedFlowView *)flowView;

	@optional
	/**
	 *  滚动到了某一列
	 *
	 *  @param pageNumber <#pageNumber description#>
	 *  @param flowView   <#flowView description#>
	 */
	- (void)didScrollToPage:(NSInteger)pageNumber inFlowView:(NewPagedFlowView *)flowView;
	
	/**
     *  点击了第几个cell
     *
     *  @param subView 点击的控件
     *  @param subIndex    点击控件的index
     *
     *  @return <#return value description#>
     */
     - (void)didSelectCell:(UIView *)subView withSubViewIndex:(NSInteger)subIndex;

	@end
	
    @protocol NewPagedFlowViewDataSource <NSObject>

    /**
    *  返回显示View的个数
    *
    *  @param flowView <#flowView description#>
    *
    *  @return <#return value description#>
    */
    - (NSInteger)numberOfPagesInFlowView:(NewPagedFlowView *)flowView;

	/**
	*  给某一列设置属性
	*
	*  @param flowView <#flowView description#>
 	*  @param index    <#index description#>
 	*  @return <#return value description#>
	*/
    - (UIView *)flowView:(NewPagedFlowView *)flowView 	cellForPageAtIndex:(NSInteger)index;

	@end

###5.代码示例
    NewPagedFlowView *pageFlowView = [[NewPagedFlowView alloc] initWithFrame:CGRectMake(0, 64, Width, (Width - 84) * 9 / 16 + 24)];
    pageFlowView.backgroundColor = [UIColor whiteColor];
    pageFlowView.delegate = self;
    pageFlowView.dataSource = self;
    pageFlowView.minimumPageAlpha = 0.4;
    pageFlowView.minimumPageScale = 0.85;
    
    //初始化pageControl
    UIPageControl *pageControl = [[UIPageControl alloc] initWithFrame:CGRectMake(0, pageFlowView.frame.size.height - 24 - 8, Width, 8)];
    pageFlowView.pageControl = pageControl;
    [pageFlowView addSubview:pageControl];
    [pageFlowView startTimer];
    [self.view addSubview:pageFlowView];
**具体含义请看源代码, Designed By Page,QQ:799573715 **