# 俩必须掌握的排序

> 问最多的俩，不会手撕就和面试官干瞪眼吧OTZ。

## 快速排序

> 面字节、腾讯都被要求手写快排啦。

```java
import java.util.*;
//快速排序
//不稳定，平均空间复杂度O(logn)，平均时间复杂度是O(nlogn)

/**
再优化，之前代码中基准数已经在pivotKey中保存了，
所以不需要每次交换都设置一个temp变量，
在交换左右指针的时候只需要先后覆盖就可以了。
这样既能减少空间的使用还能降低赋值运算的次数。
**/

public class Main{
	public static void main(String[] args){
		int[] a = new int[]{9,5,2,6,7,3,1,3,2};
		QuickSort.sort(a);
		System.out.println(Arrays.toString(a));
	}
}
class QuickSort{
	//一次划分（找到一个基准数，划分后基准数左边都比他小，右边都比他大）
	public static int partition(int[] arr,int left,int right){
		//一般设置最左边的为基准数
		int pivotKey = arr[left];
		//基准数的位置
		int pivotPointer = left; // 这个变量并没有用到，哇哈哈

		//右指针找比基准数小的，左指针找比基准数大的，然后进行交换
		while(left<right){
			// 先移动右指针，原因http://www.cnblogs.com/wxisme/p/5243631.html
			while(left<right && arr[right]>=pivotKey){
				right--;
			}
			//↑右指针找到了第一个比基准数小的数，就停止循环，并把小的数移动到左边
			arr[left] = arr[right];

			while(left<right && arr[left]<=pivotKey){
				left++;
			}
			//↑左指针找到了第一个比基准数大的数，就停止循环，并把大的数移动到右边
			arr[right] = arr[left];
		}
		// 把基准值赋值给两个指针碰头的地方，也就是中间
    // 退出上面循环的时候，left=right
		arr[left] = pivotKey; //所以left换成right一样的

		//把这个位置返回，以给下一次划分使用，划分左半边就-1，划分右半边就+1
		return left;//这里换成right也ok
	}

  // 快排
	public static void quickSort(int[] arr,int left,int right){
		if(left < right) {
      //得到第一次划分的基准数位置
      int pivotPos = partition(arr,left,right);
      //左半边继续快速排序
      quickSort(arr,left,pivotPos-1);
      //右半边继续快速排序
      quickSort(arr,pivotPos+1,right);
    }
	}

  // 排序
	public static void sort(int[] arr){
		if(arr==null||arr.length==0){
			return;
		}
    // 快排
		quickSort(arr,0,arr.length-1);
	}

  // 交换数字
	public static void swap(int[] arr,int left,int right){
		int temp = arr[left];
		arr[left] = arr[right];
		arr[right] = temp;
	}

}
```

## 归并排序

```java
import java.util.*;
// 归并排序
// 稳定，平均空间复杂度为O(n)，平均时间复杂度为O(nlogn)。
/**
其基本思想是，先递归划分子问题，然后合并结果。
把待排序列看成由两个有序的子序列，然后合并两个子序列，
.....
**/
public class Main{
	public static void main(String[] args){
		int[] a = new int[]{9,5,2,6,7,3,1,3,2};
		MergeSort.mSort(a,0,a.length-1);
		System.out.println(Arrays.toString(a));
	}
}

class MergeSort{
	public static void mergeSort(int[] arr){
    // 判空
		if(arr==null||arr.length==0){
			return;
		}
    // 归并排序
		mSort(arr,0,arr.length-1);
	}

	// 归并排序，其实就是递归分治
	public static void mSort(int[] arr,int left,int right){
    // 和快排一样，直接left<right括起来也可以
		if(left>=right)
			return;
		// 中点
		int mid = (left+right)/2; // int mid = left + (right - left) / 2;

		//递归排序左半边
		mSort(arr,left,mid);

		//递归排序右半边
		mSort(arr,mid+1,right);

		//合并
		merge(arr,left,mid,right);

	}

	//合并两个有序数组[left,mid]和[mid+1,right]
	public static void merge(int[] arr,int left,int mid,int right){
		//中间数组
    //归并排序需要用到一个临时数组
		int[] temp = new int[right-left+1];

    // 双指针，i指向第一个数组左边界，j指向第二个数组左边界
		int i = left;
		int j = mid+1;
    // 下标
		int k = 0;

    // 填满temp
		while(i<=mid&&j<=right){
			//i和j分别从两个有序数组的最左边开始遍历，谁更小就放temp里去
			if(arr[i]<=arr[j]){
        // 别忘记自增
				temp[k++] = arr[i++];
			}else{
				temp[k++] = arr[j++];
			}
		}
		//下面是while，别脑抽写成if啦
    // 而且一定是<=，试了一下 < 出错了，为什么呢？因为如果刚好指向了mid不能丢掉mid呀。要把mid加进去
		//如果第二个数组的数全部遍历完了，第一个数组还有剩，接下来直接把第一个数组的数全部加进temp即可
		while(i<=mid){
			temp[k++] = arr[i++];
		}

		//如果第一个数组的数全部遍历完了，第二个数组还有剩，接下来直接把第二个数组的数全部加进temp即可
		while(j<=right){
			temp[k++] = arr[j++];
		}

		//此时temp已经是一个合并成功的有序数组，再放回arr就好啦
		for(int p=0;p<temp.length;p++){
			arr[left+p]=temp[p];
			//注意一定是arr[left+p],不是arr[p]，merge函数的参数就是从left开始的！注意！
		}
	}
}
```

