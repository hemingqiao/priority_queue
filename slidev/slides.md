---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: https://source.unsplash.com/collection/94734566/1920x1080
background: https://pt-starimg.didistatic.com/static/starimg/img/ejVOD7es7h1620916196284.webp
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
---

# PriorityQueue - 优先队列(堆)

优先队列(堆)的相关概念和简单实现

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# 优先队列的概念

<br/>

- 📝 **优先队列是队列** 
    - 具有队列的所有性质，如元素先进先出(first in, first out)等
    - 可以认为优先队列实现了队列中的所有接口/方法
    ``` ts
    class PriorityQueue implements Queue {
        offer() {
            // 向队尾添加一个元素
        }

        poll() {
            // 从队头弹出一个元素
      	}
		
      	peek() {
        	// 查看队头元素(不会将元素从队列中弹出)
      	} 
    }
    ```

<br>
<br>
<div v-click><b>优先队列区别于普通队列的特性是什么呢？</b></div>


<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}
</style>

---

# 优先队列的概念

简而言之，优先队列就是元素具有优先级的队列，同时它可以视为堆的一种实现。

- 💻 **优先队列中的元素具有可定制的优先级** 
    - 普通队列最为显著的特点就是元素先进先出，其实也可以视为具有一定的优先级：以进入队列的时间作为出队的优先级
    - 而优先队列则是为开发者提供了可以**定制**这个元素优先级的能力，优先队列可以传入一个比较器(函数)，来比较元素之间的优先级，从而实现 first in, largest out(优先级最高的元素先出队)

    ``` ts
    const comparator = (a, b) => a - b; // 比较器函数
	const array = [2, 1, 4, 7, 4, 8, 3, 6, 4, 7];

	array.sort(comparator);
	console.log(array); // [1, 2, 3, 4, 4, 4, 6, 7, 7, 8]

    let queue = new PriorityQueue(comparator); // 定制优先队列的优先级

	for (let i = 1e9; i; i--) {
		queue.offer(Math.floor(Math.random() * i));
	}
	console.log(q.poll()); // 0
    ```

<br>
<br>



<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}
</style>

---

# 堆（Heap）

<img v-click src="https://images2015.cnblogs.com/blog/1094457/201702/1094457-20170225194935460-153137074.png" class="full-binary-tree rounded shadow" />

<p class="desc">
百科中关于堆的定义：<b>堆（heap）是计算机科学中一类特殊的数据结构的统称。</b>
<br/>
<br/>
堆总是满足下列性质：
<br />1、堆总是一棵完全二叉树。
<br />2、堆中某个结点的值总是小于等于或者是大于等于其父结点的值；
<!-- <br />3、完全二叉树除了最下面一层之外，其他所有层都是填满的(每个节点的左右子结点都有值)，最下面一层则是从左到右分布。 -->
<br />3、将根结点最大的堆叫做最大堆或大根堆，根结点最小的堆叫做最小堆或小根堆。
</p>

<p class="desc" v-click>
    <b>优先队列是堆的一种实现</b>
	<br/>
	<br/>
	有多种方式可以实现优先队列。如维护一个有序的数组，每次插入新的元素之后，对整个数组重新进行排序。
	<br/>
	但是为了保证存取元素的时间复杂度，优先队列在实现上使用了完全二叉树作为其数据存储结构，而用于实现优先队列的完全二叉树中的所有父节点的值都是大于等于或者小于等于其左右子结点的值。
</p>

    

<br>
<br>

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}

.full-binary-tree {
	width: 20rem;
	position: absolute;
	right: 1.5rem;
}

.desc {
	width: calc(100% - 21rem);
}
</style>

---

# 存储完全二叉树

<img v-click src="https://img2018.cnblogs.com/blog/1340275/201901/1340275-20190130123004165-113058710.png" class="tree-store rounded shadow" />

    

<br>
<br>

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}

.tree-store {
	width: 60%;
}
</style>
---

# Code

``` ts
class PriorityQueue {
	heap = [0]; 		// 用来存储完全二叉树
	cnt = 0;    		// 优先队列中的元素个数
	comparator = null;  // 比较器

	constructor(initialArray = [], comparator = (a, b) => a - b) {
		this.heap = this.heap.concat(initialArray);
		this.cnt = initialArray.length;
		this.comparator = comparator;
	}

	offer(x) {
		// TODO
	}

	poll() {
		// TODO
	}

	peek() {
		// TODO
	}
}
```

---

## Code

```ts
class PriorityQueue {
	heap = [0]; 		// 用来存储完全二叉树
	cnt = 0;    		// 优先队列中的元素个数
	comparator = null;  // 比较器

	down(u) {
		let t = u;
		// 与左子节点做比较
		if (u * 2 <= this.cnt && this.comparator(this.heap[u * 2], this.heap[t]) < 0) t = u * 2;
		// 与右子结点作比较
		if (u * 2 + 1 <= this.cnt && this.comparator(this.heap[u * 2 + 1], this.heap[t]) < 0) t = u * 2 + 1;
		if (t !== u) {
			swap(this.heap, u, t);
			this.down(t);
		}
	}

	poll() {
		if (this.cnt <= 0) throw new Error("queue is empty");
		let ret = this.heap[1]; // 将要出队的元素
		this.cnt--;
		this.heap[1] = this.heap.pop();
		this.down(1);
		return ret;
	}
}
```

---

# Code


```ts
class PriorityQueue {
	heap = [0]; 		// 用来存储完全二叉树
	cnt = 0;    		// 优先队列中的元素个数
	comparator = null;  // 比较器

	up(u) {
		while (u >> 1 > 0 && this.comparator(this.heap[u], this.heap[u >> 1]) < 0) {
			swap(this.heap, u >> 1, u);
			u >>= 1;
		}
	}

	offer(x) {
		this.heap.push(x);
		this.cnt++;
		this.up(this.cnt);
	}
}
```


---

# Code


```ts
class PriorityQueue {
	heap = [0]; 		// 用来存储完全二叉树
	cnt = 0;    		// 优先队列中的元素个数
	comparator = null;  // 比较器

	constructor(initialArray = [], comparator = (a, b) => a - b) {
		this.heap = this.heap.concat(initialArray);
		this.cnt = initialArray.length;
		this.comparator = comparator;
		this.heapify(); // 将初始数组`堆化`
	}

	down(u) {
		// ...
	}

	heapify() {
		for (let i = this.cnt >> 1; i; i--) {
			this.down(i);
		}
	}
}
```
---

# Code


```ts
class PriorityQueue {
	heap = [0]; 		// 用来存储完全二叉树
	cnt = 0;    		// 优先队列中的元素个数
	comparator = null;  // 比较器

	peek() {
		if (this.cnt <= 0) throw new Error("queue is empty");
		return this.heap[1];
	}

	size() {
		return this.cnt;
	}

	isEmpty() {
		return this.cnt <= 0;
	}
}
```

