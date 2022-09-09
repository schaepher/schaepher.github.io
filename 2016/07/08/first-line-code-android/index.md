# 读《第一行代码——android》



* 隐式Intent  
* Activity活动周期  
>+ 整个周期  
>+ 三个分段  
>+ onSaveInstanceState()方法  
>+ 可以将数据放在Bundle，再将Bundle存放在Intent里  

* 活动的四种启动方式  

* 知道当前是在哪一个活动  
getClass().getSimpleName()  
新建一个活动，放入该代码到Log，其他活动都继承该活动。即建立一个专门的类，把所有活动都会出现的代码都放在这里（与集合类不同）。  

* static  
>1. 集合类管理器  
	public static List<Activity\> activities = new ArrayList<Activity\>();  	
	public static void addActivity(Activity activity)  
	{  
	 activity.add(activity);  
	}
>2. 启动活动  
	public clasee SecondActivity extends Activity  
	{  
		public static void actionStart(Context context, String data1, String data2)  
		{  
			Intent intent = new Intent(context,SecondActivity.class);  
			intent.putExtra("param1",data1);  
			intent.putExtra("param2",data2);  
			context.startActivity(intent);  
		}
	}

需要启动该SecondActivity时，直接调用：  
SecondActivity.actionStart(this, "data1","data2");  


* android:maxLines="2"  
指定EditText最大行数为2行，超过2行时文本向上滚动。  

* ImageView.setImageResource(R.drawable.picture);  

* ProgressBar  
ProgressBar.getProgress()  
ProgressBar.setProgress(int)  

* ProgressDialog  

* RelativeLayout  
 android:layout_centerInParent="true"   
android:layout_alignLeft表示让一个控件的左边缘和另一个控件的左边缘对齐  

* 引入布局  
`<include layout="@layout/title" />`   


* 自定义标题栏  
public class TitleLayout extends LinearLayout { 
   
  public TitleLayout(Context context, AttributeSet attrs) { 
    super(context, attrs); 
    LayoutInflater.from(context).inflate(R.layout.title, this); 
  } 
 
} 

