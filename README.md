# 2021-05-09
排序和查找，考前突击！

一、查找：线性查找与二分查找
1、线性查找的格式：
穷举下标，遍历数组元素。分找到与未找到两种情况返回/输出。
2、二分查找
递归实现：
int BinSearch(long num[], long key, int low, int high)
{
	int mid = (high + low) / 2;
	if (low > high)//递归结束条件 
	{
		return -1;//没找到 
	}
	if (key > num[mid])
	{
		return BinSearch(num, key, mid+1, high);//在后一子表查找 
	}
	else if (key < num[mid])
	{
		return BinSearch(num, key, low, mid-1);//在前一子表查找 
	}
	return mid; //返回找到的位置下标 
}
要点：4个参数，入口处设置结束条件，递归的运用

迭代实现：
int BinSearch(long num[], long key, int n)
{
	int low = 0;
	int high = n - 1;
	int mid;
	while (low <= high)//循环继续条件
	{
		mid = (low + high) / 2;
		
		if (key > num[mid])
		{
			low = mid + 1;	//在后一子表查找 
		}
		else if (key < num[mid])
		{
			high = mid - 1; //在前一子表查找 
		}
		else
		{
			return mid;//返回找到的位置下标 
		}
	}
	return -1;//没找到
}

二、排序
1、交换排序
以升序为例
void FindMin(int x[], int n)
{
	int temp,j;
	for (i=0 ; i<n-1; i++)
	{
		//假设除了前i个数以外，x[i]最小
		for (j=i+1 ; j<n ; j++)
		{
			if (x[j] < x[i])
			{
				temp = x[j];
				x[j] = x[i];
				x[i] = temp;
			}
		}
	}
}
假设前i个数已按升序排好了，目标是将第i+1个最小数放x[i]里，找出后面所有数的最小值。
n个数，这个过程要重复n-1次。

2、选择排序
void FindMin(int x[], int n)
{
	int temp, j, k, i;
	for (i=0 ; i<n-1 ; i++)
	{
		//假设剩余序列第一个数（下标为i）最小
		k = i;
		for (j=i+1 ; j<n ; j++)
		{
			if (x[j] < x[k])
			{
				k = j;
			}
		}
		if (k != i)
		{
			temp = x[k];
			x[k] = x[i];
			x[i] = temp;
		}
	}
}

3、冒泡排序
以升序为例
void BubbleSort(int a[], int n)
{
	int i, j, temp;
	for (i=0 ; i<n-1 ; i++)
	{
		for (j=n-1 ; j>i ; j--)
		{
			if (a[j] < a[j-1])
			{
				temp = a[j-1];
				a[j-1] = a[j];
				a[j] = temp;
			}
		}
	}
}
思路：从后往前比较，小数上（前）移，比较n-1次。
或者：
void BubbleSort(int a[], int n)
{
	int i, j, temp;
	for (i=0 ; i<n-1 ; i++)
	{
		for (j=0 ; j<n-1-i ; j++)
		{
			if (a[j] > a[j+1])
			{
				temp = a[j+1];
				a[j+1] = a[j];
				a[j] = temp;
			}
		}
	}
}
思路：从前往后比较，大数下（后）移，比较n-1次。
void InsertSort(int a[], int n)
{
	int i, j, x;
	for (j=1 ; j<n ; j++)//依次将a[1],a[2]插入前面有序序列 
	{
		x = a[j];//将a[j]作为待插入的数据 
		for (i=j-1 ; i>=0 && x<a[i] ; i--)
		{
			a[i+1] = a[i];//只要x<a[i]，就将a[i]后移 
		}
		a[i+1] = x;//当x>=a[i]时，就将x插入a[i]后面 
	}
}
