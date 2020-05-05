设计一个找到数据流中第K大元素的类（class）。注意是排序后的第K大元素，不是第K个不同的元素。

你的 KthLargest 类需要一个同时接收整数 k 和整数数组nums 的构造器，它包含数据流中的初始元素。每次调用 KthLargest.add，返回当前数据流中第K大的元素。

示例:

int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
说明:
你可以假设 nums 的长度≥ k-1 且k ≥ 1。


解题思路
使用数组来构建一个容量为k的小顶堆。
如果小顶堆满后，再添加元素，那么直接和堆顶元素进行比较。
2.1 如果大于堆顶元素，则重建堆；
2.2 如果小于或等于堆顶元素，则忽略。
heap[0]就是第k个最大元素
代码
class KthLargest {

    int[] heap;

    //heap数组中实际存放的元素数量
    int size = 0;

    public KthLargest(int k, int[] nums) {
        heap = new int[k];
        for (int num : nums) {
            add(num);
        }
    }

    public int add(int val) {
        if (size < heap.length) {
            size++;
            heap[size - 1] = val;

            if (size == heap.length) {
                //构建小顶堆
                makeMinHeap();
            }

        } else {
            if (heap[0] < val) {
                //替换堆顶元素
                heap[0] = val;
                minHeapFixdown(0);
            }
        }

        return heap[0];
    }

    /**
     * 堆化heap数组，建立最小堆
     */
    private void makeMinHeap() {
        int length = heap.length;
        //第一个非叶子节点为什么是(length / 2) - 1呢？
        for (int i = (length / 2) - 1; i >= 0; i--) {
            minHeapFixdown(i);
        }
    }

    /**
     * 从i节点开始调整, i节点的子节点为 2*i+1, 2*i+2
     *
     * @param i 第i个节点
     */
    public void minHeapFixdown(int i) {
        int temp = heap[i];
        //子节点是多少？i节点的子节点为 2*i+1, 2*i+2
        int subLeft = 2 * i + 1;
        while (subLeft < heap.length) {
            int subRight = subLeft + 1;
            if (subRight < heap.length && heap[subLeft] > heap[subRight]) {
                subLeft++;
            }

            if (heap[subLeft] >= heap[i]) {
                break;
            }
            heap[i] = heap[subLeft];
            heap[subLeft] = temp;

            i = subLeft;
            subLeft = 2 * i + 1;
        }

    }
}

作者：wang_dong
链接：https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/solution/3ge-bu-zou-jian-dan-yi-dong-tong-guo-xiao-ding-dui/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


关于 Java 的 PriorityQueue 优先级队列
1 是线程不安全的队列
2 存储使用数组实现
3 利用比较器做优先级比较

实现说明
1 最小堆的特性就是最小的值在最上面，每次取O(1)，插入O(n)
2 初始化的时候，注意如何添加元素，并给队列一个合适大小的初值
3 每次添加元素，能添加到队列的有两种情况，一种未到k个，另一种比堆顶大

实现代码

public class KthLargest {

    private PriorityQueue<Integer> queue;
    private int limit;

    public KthLargest(int k, int[] nums) {
        limit = k;
        queue = new PriorityQueue<>(k);
        for (int num : nums) {
            add(num);
        }
    }

    public int add(int val) {
        if (queue.size() < limit) {
            queue.add(val);
        } else if (val > queue.peek()) {
            queue.poll();
            queue.add(val);
        }

        return queue.peek();
    }

}
单元测试

class KthLargestTest {

    @Test
    void add() {
        int k = 3;
        int[] arr = new int[] { 4, 5, 8, 2 };
        KthLargest kthLargest = new KthLargest(k, arr);
        assertEquals(4, kthLargest.add(3));
        assertEquals(5, kthLargest.add(5));
        assertEquals(5, kthLargest.add(10));
        assertEquals(8, kthLargest.add(9));
        assertEquals(8, kthLargest.add(4));
    }
}

作者：wang-zi-hao-zain
链接：https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/solution/javashi-yong-zui-xiao-dui-lai-shi-xian-shi-yong-ne/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。