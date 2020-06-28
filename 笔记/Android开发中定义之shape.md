	<?xml version="1.0" encoding="utf-8"?>
	<shape
	    xmlns:android="http://schemas.android.com/apk/res/android"
	    android:shape=["rectangle" | "oval" | "line" | "ring"]      //共有4种类型，矩形（默认）/椭圆形/直线形/环形
	    // 以下4个属性只有当类型为环形时才有效
	    android:innerRadius="dimension"     //内环半径
	    android:innerRadiusRatio="float"    //内环半径相对于环的宽度的比例，比如环的宽度为50,比例为2.5,那么内环半径为20
	    android:thickness="dimension"   //环的厚度
	    android:thicknessRatio="float"     //环的厚度相对于环的宽度的比例
	    android:useLevel="boolean">    //如果当做是LevelListDrawable使用时值为true，否则为false.
	
	    <corners    //定义圆角
	        android:radius="dimension"      //全部的圆角半径
	        android:topLeftRadius="dimension"   //左上角的圆角半径
	        android:topRightRadius="dimension"  //右上角的圆角半径
	        android:bottomLeftRadius="dimension"    //左下角的圆角半径
	        android:bottomRightRadius="dimension" />    //右下角的圆角半径
	
	    <gradient   //定义渐变效果
	        android:type=["linear" | "radial" | "sweep"]    //共有3中渐变类型，线性渐变（默认）/放射渐变/扫描式渐变
	        android:angle="integer"     //渐变角度，必须为45的倍数，0为从左到右，90为从上到下
	        android:centerX="float"     //渐变中心X的相当位置，范围为0～1
	        android:centerY="float"     //渐变中心Y的相当位置，范围为0～1
	        android:startColor="color"      //渐变开始点的颜色
	        android:centerColor="color"     //渐变中间点的颜色，在开始与结束点之间
	        android:endColor="color"    //渐变结束点的颜色
	        android:gradientRadius="float"  //渐变的半径，只有当渐变类型为radial时才能使用
	        android:useLevel=["true" | "false"] />  //使用LevelListDrawable时就要设置为true。设为false时才有渐变效果
	
	    <padding    //内部边距
	        android:left="dimension"
	        android:top="dimension"
	        android:right="dimension"
	        android:bottom="dimension" />
	
	    <size   //自定义的图形大小
	        android:width="dimension"
	        android:height="dimension" />
	
	    <solid  //内部填充颜色
	        android:color="color" />
	
	    <stroke     //描边
	        android:width="dimension"   //描边的宽度
	        android:color="color"   //描边的颜色
	        // 以下两个属性设置虚线
	        android:dashWidth="dimension"   //虚线的宽度，值为0时是实线
	        android:dashGap="dimension" />      //虚线的间隔
	</shape>