#### Android 查遗补缺
上层控件负责下层子控件的测量和绘制，并传递交互事件
自定义view时 重要的方法 onMeasure() onLayout() onDraw() onTouchEvent() onInterceptTouchEvent() computeScroll()  onFinishInflate()  onSizeChanged()
默认onMeasure()方法只支持EXACTLY模式
关键点重新确定控件的大小 setMeasuredDimension()

Canvas canvas = new Canvas(bitmap);推荐使用bitmap构造方法。
传进去的bitmap与通过这个bitmap创建的canvas是紧密联系在一起的，这个过程我们称之为装载画布

xmlns:android="http://schemas.android.com/apk/res/android"
这行代码就是在指定引用的 名字空间xmlns,即xml namespace。这里指定了名字空间为“android”，因此在接下来
使用系统属性的时候，才可以使用“android:”来应用Android的系统属性。
如果使用自定义的属性，那么就需要创建自己的名字空间，在Android Studio中，第三方控件都使用如下的代码来引入名字空间
xmlns:app="http://schemas.android.com/apk/res-auto"(app:attributes)
xmlns:custom="http://schemas.android.com/apk/res-auto"(custom:attributes)

获取文本宽高 top  ascent baseline descent bottom
 Rect rect = new Rect();
 mPaint.getTextBounds(text,0,text.length(), rect);
 canvas.drawRect(rect, mPaint);
float textHeight1 = rect.height();

在计算机图形领域，一个 Shader 是指一段用来着色的计算机程序，通常用来生成一张图片中适当等级的颜色值，
或者是生成特殊的视觉效果，或者是对视频画面进行处理。对于非专业人士的角度来看，它可以被描述为–“一种告诉
计算机怎么样通过某种特殊手段绘制一些图像的程序”。
shader BitmapShader  ComposeShader LinearGradient RadialGradient SweepGradient 
Shader.TileModel CLAMP(边缘延展) MIRROR REPEAT

Android坐标系（屏幕左上角原点）getRawX(), getRawY(); 视图坐标系（父视图左上角原点）getX(), getY();

scrollBy()(偏移量)  scrollTo()(到点) 注：移动的是View的content，即让view的内容移动，如果在View Group中使用则移动
的是所有子view， 但在View中，移动的将是内容
scroller computeScrollOffset() 是否完成了整体滑动

几种图形
RectShape RoundRectShape（绘制自定义圆角个数的圆角框） OvalShape ArcShape

xml shape
oval（椭圆）  rectangle(矩形，corners)
line(跨越包含视图宽度的水平线。此形状需要 <stroke> 元素定义线宽)  
ring(特有属性 android:innerRadius  android:thickness) 

canavas 画布
save() 保存图层 restore() 合并图层
translate() 平移画布 rotate() 旋转画布 ---坐标轴的移动和旋转
drawBitmapMesh(@NonNull Bitmap bitmap<将要扭曲的图像>, int meshWidth<需要的横向网格数>, int meshHeight<需要的纵向网格数>,
            @NonNull float[] verts<网格交叉点坐标数>, int vertOffset<数组中开始跳过的（x, y）坐标数>, @Nullable int[] colors, int colorOffset,
            @Nullable Paint paint)

ColorMatrix 颜色矩阵(5 * 5)
setRotate(int axis, float degree) 色调（axis 0, 1, 2代表red, green, blue）(degree, 处理的色调)
setSaturation(float sat) 饱和度 （0， 灰度图像, 1, 饱和）
setScale(float rScale<红色>, float gScale<绿色>, float bScale<蓝色>, float aScale<透明度>)亮度 （0， 全黑）
postConcat() 混合多种效果

对图像做特殊处理时常用的方法，对图像像素点做处理
Bitmap getPixes(oldPx, 0, width, 0, 0, width, height) setPixes(oldPx, 0, width, 0, 0, width, height)
Color.red() Color.green() Color.blue() 解释：颜色由红绿蓝混合而成，方法分别对应了各个颜色对应的值

图像特效处理
Matrix  setTranslate() 平移，setRotate(),  setScale() 缩放， setSkew() 错切
matrix.setScale(1, -1);实现图像垂直翻转
pre() post() 提供矩阵的前乘和后乘运算

PorterDuffXfermode 设置的是两个图层交集区域显示方式
抠图两种方式 第一种PorterDuffXfermode 第二种 BitmapShader
PorterDuff.Mode 常用 SRC_IN, DST_IN
Shader（填充）,    BitmapShader, LinearGradient, RadialGradient, SweepGradient, ComposeShader
PathEffect（线形） CornerPathEffect（拐角圆滑）, DiscretePathEffect, DashPathEffect,  PathDashPathEffect（自定义间隔类型虚线）, ComposePathEffect

Android 系统通过发出VSYNC信号来进行屏幕的重绘，间隔16ms(即60帧)
view          主动更新              主线程      没有双缓存
surfaceview   被动更新（频繁刷新）  通常子线程  底层实现双缓存

SurfaceView 自定义模板
~~~
public class MySurfaceView extends SurfaceView implements SurfaceHolder.Callback, Runnable{

    public MySurfaceView(Context context) {
        super(context);
        init();
    }

    public MySurfaceView(Context context, AttributeSet attrs) {
        super(context, attrs);
        init();
    }

    //SurfaceHolder
    private SurfaceHolder mHolder;
    //绘图画布
    private Canvas mCanvas;
    //子线程标志位
    private boolean isDrawing;
    
    private void init() {
        mHolder = getHolder();
        mHolder.addCallback(this);
        setFocusable(true);
        setFocusableInTouchMode(true);
        this.setKeepScreenOn(true);
    }
    

    @Override
    public void surfaceCreated(SurfaceHolder holder) {
        new Thread(this).start();
    }

    @Override
    public void surfaceChanged(SurfaceHolder holder, int format, int width, int height) {

    }

    @Override
    public void surfaceDestroyed(SurfaceHolder holder) {
        isDrawing = false;
    }

    @Override
    public void run() {
        while (isDrawing) {
            draw();
        }
    }
    
    private void draw() {
        try {
            mCanvas = mHolder.lockCanvas();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if(mCanvas != null) {
                mHolder.unlockCanvasAndPost(mCanvas);
            }
        }
    }
}

~~~

动画 
视图动画(无交互) xml set scale translate rotate alpha
属性动画(操纵的属性必须有get,set方法) xml set value-animator object-animator
常见的属性方法，translationX, translationY, rotation, rotationX, rotationY, scaleX, scaleY, pivotX, pivotY, x, y alpha, 
PropertyValuesHolder 针对同一个对象的多个属性同时作用多种动画
ValueAnimator -- 数值发生器
~~~
                //一个样例
                ValueAnimator animator = ValueAnimator.ofFloat(0, 100);
                animator.setTarget(button);
                animator.setDuration(300).start();
                animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
                    @Override
                    public void onAnimationUpdate(ValueAnimator animation) {
                        Float value = (Float) animation.getAnimatedValue();
                        ConstraintLayout.MarginLayoutParams params = (ConstraintLayout.MarginLayoutParams) button.getLayoutParams();
                        params.leftMargin += value;
                        button.setLayoutParams(params);
                    }
                });
~~~
布局动画 在布局中添加好用android:animateLayoutChanges="true"
~~~
        //布局动画代码样例
        FrameLayout layout = findViewById(R.id.layout);
        ScaleAnimation scale = new ScaleAnimation(3, 1, 3, 1);
        scale.setDuration(2000);
        LayoutAnimationController controller = new LayoutAnimationController(scale, 0.5f);
        controller.setOrder(LayoutAnimationController.ORDER_NORMAL);
        layout.setLayoutAnimation(controller);
~~~
插值器(定义动画变换速率) 常用插值器 LinearInterpolator，AccelerateInterpolator, DecelerateInterpolator
SVG(Scalable Vector Graphics) 可伸缩矢量图形




