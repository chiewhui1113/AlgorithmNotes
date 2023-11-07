# 找第K大的元素（LeetCode 215）
1. K多大就建立多大的堆
2. 找最大用小堆
3. 只有比根元素大才进堆
```Java
public int findKthLargest(int[] nums, int k) {
  if (k > nums.length) return -1;
  int len = nums.length;
  PriorityQueue<Integer> minHeap = new PriorityQueue<>(k, (a, b) -> a - b);
  for (int i = 0; i < k; i++) {
      minHeap.add(nums[i]);
  }
  for (int i = k; i < len; i++) {
      Integer topele = minHeap.peek();
      if (nums[i] > topele) {
          minHeap.poll();
          minHeap.offer(nums[i]);
      }
  }
  return minHeap.peek();
}
```

## 堆排序原理
升序用小，降序用大。由于堆顶一顶是最大/最小的元素，只要依次删除加进res里面，再调整，堆顶就是第二大/第二小的元素了。

## 合并K个链表（LeetCode 23）
```Java
public ListNode mergeKLists(ListNode[] lists) {
  if (lists == null || lists.length == 0) return null;
  PriorityQueue<ListNode> q = new PriorityQueue<> (Comparator.comparing(node->node.val));
  for (int i = 0; i < lists.length; i++) {
      if (lists[i] != null) {
          q.add(lists[i]);
      }
  }

  ListNode dummy = new ListNode(0);
  ListNode tail = dummy;

  while (!q.isEmpty()) {
      tail.next = q.poll();
      tail = tail.next;
      if (tail.next != null) {
          q.add(tail.next);
      }
  }
  
  return dummy.next;
}
```

## 数据流的中位数（LeetCode 295）
```Java
class MedianFinder {
  PriorityQueue<Integer> minHeap;
  PriorityQueue<Integer> maxHeap;

  public MedianFinder() {
      this.minHeap = new PriorityQueue<>();
      this.maxHeap = new PriorityQueue<>((a, b) -> b - a);
  }
  
  public void addNum(int num) {
      if (minHeap.isEmpty() || num > minHeap.peek()) {
          minHeap.offer(num);
          if (minHeap.size() - maxHeap.size() > 1) {
              maxHeap.offer(minHeap.poll());
          }
      } else {
          maxHeap.offer(num);
          if (maxHeap.size() - minHeap.size() > 0) {
              minHeap.offer(maxHeap.poll());
          }
      }
  }
  
  public double findMedian() {
      if (minHeap.size() > maxHeap.size()) {
          return minHeap.peek();
      } else if (minHeap.size() < maxHeap.size()) {
          return maxHeap.peek();
      } else {
          return (minHeap.peek() + maxHeap.peek()) / 2.0;
      }
  }
}
```
