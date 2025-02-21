### **3.1 PHP’de bağlı liste (linked list) nasıl oluşturulur?**  
✍ **Cevap:**  
PHP'de bağlı liste oluşturmak için sınıf (class) kullanabiliriz. Her düğüm (node) bir nesne olarak temsil edilir ve bu nesneler birbirine bağlanır. Örnek bir bağlı liste oluşturma kodu:

```php
class Node {
    public $data;
    public $next;

    public function __construct($data) {
        $this->data = $data;
        $this->next = null;
    }
}

class LinkedList {
    public $head;

    public function __construct() {
        $this->head = null;
    }

    public function insert($data) {
        $newNode = new Node($data);
        if ($this->head === null) {
            $this->head = $newNode;
        } else {
            $current = $this->head;
            while ($current->next !== null) {
                $current = $current->next;
            }
            $current->next = $newNode;
        }
    }
}

$list = new LinkedList();
$list->insert(10);
$list->insert(20);
$list->insert(30);
```

---

### **3.2 Büyük veri işlemleri için PHP’de en verimli veri yapıları nelerdir?**  
✍ **Cevap:**  
Büyük veri işlemleri için PHP'de aşağıdaki veri yapıları kullanılabilir:
- **Diziler (Arrays):** PHP'deki diziler dinamik olarak büyüyebilir ve verimli bir şekilde eleman ekleme, silme ve erişim sağlar.
- **Hash Table (Associative Arrays):** Anahtar-değer çiftleri için kullanılır ve O(1) zaman karmaşıklığı ile erişim sağlar.
- **SplHeap ve SplPriorityQueue:** Büyük veri setlerinde sıralama ve öncelikli işlemler için kullanılır.
- **Veritabanı Bağlantıları:** Büyük veriler için veritabanı kullanımı daha uygun olabilir.

---

### **3.3 Binary Search algoritmasını PHP’de nasıl uygularsınız?**  
✍ **Cevap:**  
Binary Search, sıralı bir dizide arama yapmak için kullanılır. Örnek bir uygulama:

```php
function binarySearch($arr, $target) {
    $low = 0;
    $high = count($arr) - 1;

    while ($low <= $high) {
        $mid = (int)(($low + $high) / 2);
        if ($arr[$mid] === $target) {
            return $mid;
        } elseif ($arr[$mid] < $target) {
            $low = $mid + 1;
        } else {
            $high = $mid - 1;
        }
    }
    return -1; // Hedef bulunamadı
}

$arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
echo binarySearch($arr, 5); // Çıktı: 4
```

---

### **3.4 Recursive (özyinelemeli) fonksiyon kullanarak Fibonacci serisini hesaplayan bir fonksiyon yazınız.**  
✍ **Cevap:**  
Fibonacci serisini recursive olarak hesaplama:

```php
function fibonacci($n) {
    if ($n <= 1) {
        return $n;
    }
    return fibonacci($n - 1) + fibonacci($n - 2);
}

echo fibonacci(10); // Çıktı: 55
```

---

### **3.5 PHP’de Stack (yığın) ve Queue (kuyruk) veri yapıları nasıl oluşturulur?**  
✍ **Cevap:**  
**Stack (Yığın):**
```php
$stack = new SplStack();
$stack->push(10);
$stack->push(20);
echo $stack->pop(); // Çıktı: 20
```

**Queue (Kuyruk):**
```php
$queue = new SplQueue();
$queue->enqueue(10);
$queue->enqueue(20);
echo $queue->dequeue(); // Çıktı: 10
```

---

### **3.6 PHP’de Hash Table nasıl çalışır?**  
✍ **Cevap:**  
PHP'de Hash Table, associative array olarak uygulanır. Anahtar-değer çiftlerini depolar ve anahtarlar üzerinde hash fonksiyonu uygulanarak hızlı erişim sağlanır. Örnek:

```php
$hashTable = [];
$hashTable["anahtar1"] = "değer1";
$hashTable["anahtar2"] = "değer2";
echo $hashTable["anahtar1"]; // Çıktı: değer1
```

---

### **3.7 Büyük veri setlerinde bellek yönetimi nasıl optimize edilir?**  
✍ **Cevap:**  
- **Veri parçalama (Chunking):** Büyük verileri küçük parçalara bölerek işlemek.
- **Lazy Loading:** Verileri sadece ihtiyaç duyulduğunda yüklemek.
- **Veritabanı indeksleme:** Sorguları hızlandırmak için indeksler kullanmak.
- **Garbage Collection:** Kullanılmayan bellek alanlarını temizlemek.

---

### **3.8 PHP’de Trie (Prefix Tree) veri yapısını nasıl oluşturur ve hangi durumlarda kullanırsınız?**  
✍ **Cevap:**  
Trie, özellikle string işlemleri ve önek aramaları için kullanılır. Örnek bir Trie yapısı:

```php
class TrieNode {
    public $children = [];
    public $isEndOfWord = false;
}

class Trie {
    private $root;

    public function __construct() {
        $this->root = new TrieNode();
    }

    public function insert($word) {
        $node = $this->root;
        for ($i = 0; $i < strlen($word); $i++) {
            $char = $word[$i];
            if (!isset($node->children[$char])) {
                $node->children[$char] = new TrieNode();
            }
            $node = $node->children[$char];
        }
        $node->isEndOfWord = true;
    }
}
```

---

### **3.9 PHP’de Breadth-First Search (BFS) ve Depth-First Search (DFS) nasıl uygulanır?**  
✍ **Cevap:**  
**BFS:**
```php
function bfs($graph, $start) {
    $visited = [];
    $queue = new SplQueue();
    $queue->enqueue($start);
    $visited[$start] = true;

    while (!$queue->isEmpty()) {
        $node = $queue->dequeue();
        echo $node . " ";
        foreach ($graph[$node] as $neighbor) {
            if (!isset($visited[$neighbor])) {
                $visited[$neighbor] = true;
                $queue->enqueue($neighbor);
            }
        }
    }
}
```

**DFS:**
```php
function dfs($graph, $start, &$visited = []) {
    $visited[$start] = true;
    echo $start . " ";
    foreach ($graph[$start] as $neighbor) {
        if (!isset($visited[$neighbor])) {
            dfs($graph, $neighbor, $visited);
        }
    }
}
```

---

### **3.10 PHP’de Graph veri yapısını nasıl temsil edersiniz? (Adjacency List & Matrix)**  
✍ **Cevap:**  
**Adjacency List:**
```php
$graph = [
    'A' => ['B', 'C'],
    'B' => ['A', 'D'],
    'C' => ['A', 'D'],
    'D' => ['B', 'C']
];
```

**Adjacency Matrix:**
```php
$graph = [
    [0, 1, 1, 0],
    [1, 0, 0, 1],
    [1, 0, 0, 1],
    [0, 1, 1, 0]
];
```

---

### **3.11 PHP’de Dijkstra algoritmasını nasıl uygularsınız?**  
✍ **Cevap:**  
Dijkstra algoritması, en kısa yol problemi için kullanılır. Örnek:

```php
function dijkstra($graph, $start) {
    $distances = [];
    $visited = [];
    $queue = new SplPriorityQueue();

    foreach ($graph as $vertex => $adj) {
        $distances[$vertex] = INF;
    }
    $distances[$start] = 0;
    $queue->insert($start, 0);

    while (!$queue->isEmpty()) {
        $current = $queue->extract();
        if (!isset($visited[$current])) {
            $visited[$current] = true;
            foreach ($graph[$current] as $neighbor => $weight) {
                $alt = $distances[$current] + $weight;
                if ($alt < $distances[$neighbor]) {
                    $distances[$neighbor] = $alt;
                    $queue->insert($neighbor, -$alt);
                }
            }
        }
    }
    return $distances;
}
```

---

### **3.12 PHP’de Merge Sort ve Quick Sort algoritmalarını karşılaştırın ve uygulayın.**  
✍ **Cevap:**  
**Merge Sort:**
```php
function mergeSort($arr) {
    if (count($arr) <= 1) {
        return $arr;
    }
    $mid = (int)(count($arr) / 2);
    $left = array_slice($arr, 0, $mid);
    $right = array_slice($arr, $mid);
    return merge(mergeSort($left), mergeSort($right));
}

function merge($left, $right) {
    $result = [];
    while (count($left) > 0 && count($right) > 0) {
        if ($left[0] < $right[0]) {
            $result[] = array_shift($left);
        } else {
            $result[] = array_shift($right);
        }
    }
    return array_merge($result, $left, $right);
}
```

**Quick Sort:**
```php
function quickSort($arr) {
    if (count($arr) <= 1) {
        return $arr;
    }
    $pivot = $arr[0];
    $left = $right = [];
    for ($i = 1; $i < count($arr); $i++) {
        if ($arr[$i] < $pivot) {
            $left[] = $arr[$i];
        } else {
            $right[] = $arr[$i];
        }
    }
    return array_merge(quickSort($left), [$pivot], quickSort($right));
}
```

---

### **3.13 PHP’de Priority Queue (öncelikli kuyruk) nasıl uygulanır?**  
✍ **Cevap:**  
PHP'de `SplPriorityQueue` sınıfı kullanılır:

```php
$pq = new SplPriorityQueue();
$pq->insert('Task 1', 3);
$pq->insert('Task 2', 1);
$pq->insert('Task 3', 2);

while (!$pq->isEmpty()) {
    echo $pq->extract() . "\n";
}
```

---

### **3.14 PHP’de Red-Black Tree veya AVL Tree gibi dengeli ağaç yapıları nasıl uygulanır?**  
✍ **Cevap:**  
PHP'de bu tür veri yapıları genellikle kütüphanelerle uygulanır. Örneğin, `SplTree` veya özel bir sınıf yazılabilir. Ancak, PHP'de bu tür yapılar genellikle manuel olarak uygulanmaz.

---

### **3.15 PHP’de JSON ve XML veri yapıları arasında performans farkları nelerdir?**  
✍ **Cevap:**  
- **JSON:** Daha hızlıdır, daha az bellek kullanır ve daha kolay parse edilir.
- **XML:** Daha yavaştır, daha fazla bellek kullanır ve daha karmaşıktır. Ancak, daha esnek ve genişletilebilir bir yapı sunar.

---

### **3.16 PHP’de Bloom Filter veri yapısını nasıl oluşturur ve hangi senaryolarda kullanırsınız?**  
✍ **Cevap:**  
Bloom Filter, büyük veri setlerinde bir elemanın var olup olmadığını kontrol etmek için kullanılır. Örnek:

```php
class BloomFilter {
    private $size;
    private $filter;

    public function __construct($size) {
        $this->size = $size;
        $this->filter = array_fill(0, $size, false);
    }

    public function add($item) {
        $hash1 = crc32($item) % $this->size;
        $hash2 = md5($item) % $this->size;
        $this->filter[$hash1] = true;
        $this->filter[$hash2] = true;
    }

    public function contains($item) {
        $hash1 = crc32($item) % $this->size;
        $hash2 = md5($item) % $this->size;
        return $this->filter[$hash1] && $this->filter[$hash2];
    }
}
```

---

### **3.17 PHP’de Sliding Window algoritmasını nasıl uygularsınız?**  
✍ **Cevap:**  
Sliding Window, ardışık alt dizilerde işlem yapmak için kullanılır. Örnek:

```php
function slidingWindow($arr, $k) {
    $n = count($arr);
    $maxSum = 0;
    for ($i = 0; $i < $k; $i++) {
        $maxSum += $arr[$i];
    }
    $windowSum = $maxSum;
    for ($i = $k; $i < $n; $i++) {
        $windowSum += $arr[$i] - $arr[$i - $k];
        $maxSum = max($maxSum, $windowSum);
    }
    return $maxSum;
}
```

---

### **3.18 PHP’de LRU (Least Recently Used) Cache nasıl uygulanır?**  
✍ **Cevap:**  
LRU Cache, en az kullanılan elemanları bellekten çıkarmak için kullanılır. Örnek:

```php
class LRUCache {
    private $capacity;
    private $cache = [];
    private $order = [];

    public function __construct($capacity) {
        $this->capacity = $capacity;
    }

    public function get($key) {
        if (isset($this->cache[$key])) {
            unset($this->order[array_search($key, $this->order)]);
            array_push($this->order, $key);
            return $this->cache[$key];
        }
        return -1;
    }

    public function put($key, $value) {
        if (isset($this->cache[$key])) {
            unset($this->order[array_search($key, $this->order)]);
        } elseif (count($this->cache) >= $this->capacity) {
            $oldest = array_shift($this->order);
            unset($this->cache[$oldest]);
        }
        $this->cache[$key] = $value;
        array_push($this->order, $key);
    }
}
```

---

### **3.19 PHP’de Büyük O (Big O) notasyonu ile algoritmaların zaman/mekân karmaşıklığını nasıl değerlendirirsiniz?**  
✍ **Cevap:**  
Big O notasyonu, algoritmaların performansını değerlendirmek için kullanılır. Örneğin:
- **O(1):** Sabit zaman karmaşıklığı.
- **O(n):** Doğrusal zaman karmaşıklığı.
- **O(n^2):** Karesel zaman karmaşıklığı.
- **O(log n):** Logaritmik zaman karmaşıklığı.

---

### **3.20 PHP’de Dynamic Programming (dinamik programlama) nasıl uygulanır? Örnek veriniz.**  
✍ **Cevap:**  
Dinamik programlama, alt problemlerin çözümlerini saklayarak karmaşıklığı azaltır. Örnek olarak Fibonacci serisi:

```php
function fibonacciDP($n, &$memo = []) {
    if ($n <= 1) {
        return $n;
    }
    if (!isset($memo[$n])) {
        $memo[$n] = fibonacciDP($n - 1, $memo) + fibonacciDP($n - 2, $memo);
    }
    return $memo[$n];
}

echo fibonacciDP(10); // Çıktı: 55
```



### **3.21 PHP’de bir diziyi tersine çeviren bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function reverseArray($arr) {
    return array_reverse($arr);
}

$arr = [1, 2, 3, 4, 5];
print_r(reverseArray($arr)); // Çıktı: [5, 4, 3, 2, 1]
```

---

### **3.22 PHP’de bir dizinin elemanlarının toplamını hesaplayan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function arraySum($arr) {
    return array_sum($arr);
}

$arr = [1, 2, 3, 4, 5];
echo arraySum($arr); // Çıktı: 15
```

---

### **3.23 PHP’de bir dizinin en büyük elemanını bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function findMax($arr) {
    return max($arr);
}

$arr = [10, 20, 5, 30, 15];
echo findMax($arr); // Çıktı: 30
```

---

### **3.24 PHP’de bir dizinin en küçük elemanını bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function findMin($arr) {
    return min($arr);
}

$arr = [10, 20, 5, 30, 15];
echo findMin($arr); // Çıktı: 5
```

---

### **3.25 PHP’de bir dizinin ortalamasını hesaplayan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function arrayAverage($arr) {
    return array_sum($arr) / count($arr);
}

$arr = [10, 20, 30, 40, 50];
echo arrayAverage($arr); // Çıktı: 30
```

---

### **3.26 PHP’de bir dizideki tek sayıları filtreleyen bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function filterOddNumbers($arr) {
    return array_filter($arr, function($item) {
        return $item % 2 !== 0;
    });
}

$arr = [1, 2, 3, 4, 5, 6];
print_r(filterOddNumbers($arr)); // Çıktı: [1, 3, 5]
```

---

### **3.27 PHP’de bir dizideki çift sayıları filtreleyen bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function filterEvenNumbers($arr) {
    return array_filter($arr, function($item) {
        return $item % 2 === 0;
    });
}

$arr = [1, 2, 3, 4, 5, 6];
print_r(filterEvenNumbers($arr)); // Çıktı: [2, 4, 6]
```

---

### **3.28 PHP’de bir diziyi rastgele karıştıran bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function shuffleArray($arr) {
    shuffle($arr);
    return $arr;
}

$arr = [1, 2, 3, 4, 5];
print_r(shuffleArray($arr)); // Örnek Çıktı: [3, 1, 5, 2, 4]
```

---

### **3.29 PHP’de bir dizide belirli bir değerin kaç kez tekrarlandığını bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function countValue($arr, $value) {
    return array_count_values($arr)[$value] ?? 0;
}

$arr = [1, 2, 3, 2, 4, 2, 5];
echo countValue($arr, 2); // Çıktı: 3
```

---

### **3.30 PHP’de bir dizinin elemanlarını string olarak birleştiren bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function arrayToString($arr) {
    return implode(", ", $arr);
}

$arr = ["PHP", "JavaScript", "Python"];
echo arrayToString($arr); // Çıktı: PHP, JavaScript, Python
```


### **3.31 PHP’de bir metindeki kelime sayısını hesaplayan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function countWords($text) {
    return str_word_count($text);
}

$text = "Merhaba dünya, bu bir test metnidir.";
echo countWords($text); // Çıktı: 6
```

---

### **3.32 PHP’de bir metindeki cümle sayısını hesaplayan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function countSentences($text) {
    return preg_match_all('/[.!?]/', $text);
}

$text = "Merhaba! Bu bir test. Nasılsın?";
echo countSentences($text); // Çıktı: 3
```

---

### **3.33 PHP’de bir metindeki en uzun kelimeyi bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function findLongestWord($text) {
    $words = explode(" ", $text);
    $longest = "";
    foreach ($words as $word) {
        if (strlen($word) > strlen($longest)) {
            $longest = $word;
        }
    }
    return $longest;
}

$text = "PHP web uygulamaları geliştirmek için harika bir dildir.";
echo findLongestWord($text); // Çıktı: uygulamaları
```

---

### **3.34 PHP’de bir metindeki tekrar eden kelimeleri bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function findRepeatedWords($text) {
    $words = str_word_count($text, 1);
    $wordCounts = array_count_values($words);
    $repeatedWords = array_filter($wordCounts, function($count) {
        return $count > 1;
    });
    return array_keys($repeatedWords);
}

$text = "PHP PHP web web uygulamaları geliştirmek için harika bir dildir.";
print_r(findRepeatedWords($text)); // Çıktı: ["PHP", "web"]
```

---

### **3.35 PHP’de bir metindeki URL’leri tespit eden bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function extractUrls($text) {
    preg_match_all('/https?:\/\/[^\s]+/', $text, $matches);
    return $matches[0];
}

$text = "Web sitemizi ziyaret edin: https://example.com. Daha fazla bilgi için: http://example.org.";
print_r(extractUrls($text)); // Çıktı: ["https://example.com", "http://example.org"]
```

---

### **3.36 PHP’de bir metindeki e-posta adreslerini tespit eden bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function extractEmails($text) {
    preg_match_all('/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/', $text, $matches);
    return $matches[0];
}

$text = "Bize ulaşın: info@example.com veya support@example.org.";
print_r(extractEmails($text)); // Çıktı: ["info@example.com", "support@example.org"]
```

---

### **3.37 PHP’de bir metindeki hashtag’leri tespit eden bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function extractHashtags($text) {
    preg_match_all('/#\w+/', $text, $matches);
    return $matches[0];
}

$text = "Bu bir #test metni. #PHP harika bir dil!";
print_r(extractHashtags($text)); // Çıktı: ["#test", "#PHP"]
```

---

### **3.38 PHP’de bir metindeki özel karakterleri temizleyen bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function sanitizeText($text) {
    return preg_replace('/[^a-zA-Z0-9\s]/', '', $text);
}

$text = "Bu bir test! @#%&*() metni.";
echo sanitizeText($text); // Çıktı: "Bu bir test  metni"
```

---

### **3.39 PHP’de bir metindeki boşlukları kaldıran bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function removeSpaces($text) {
    return str_replace(" ", "", $text);
}

$text = "Bu bir test metni.";
echo removeSpaces($text); // Çıktı: "Bubirtestmetni."
```

---

### **3.40 PHP’de bir metindeki ilk harfleri büyük yapan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function capitalizeWords($text) {
    return ucwords($text);
}

$text = "bu bir test metni.";
echo capitalizeWords($text); // Çıktı: "Bu Bir Test Metni."
```

---

### **3.41 PHP’de bir metindeki tüm harfleri büyük yapan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function toUpperCase($text) {
    return strtoupper($text);
}

$text = "Bu bir test metni.";
echo toUpperCase($text); // Çıktı: "BU BIR TEST METNI."
```

---

### **3.42 PHP’de bir metindeki tüm harfleri küçük yapan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function toLowerCase($text) {
    return strtolower($text);
}

$text = "Bu Bir Test Metni.";
echo toLowerCase($text); // Çıktı: "bu bir test metni."
```

---

### **3.43 PHP’de bir metindeki belirli bir kelimeyi değiştiren bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function replaceWord($text, $oldWord, $newWord) {
    return str_replace($oldWord, $newWord, $text);
}

$text = "Bu bir test metni.";
echo replaceWord($text, "test", "örnek"); // Çıktı: "Bu bir örnek metni."
```

---

### **3.44 PHP’de bir metindeki belirli bir karakteri kaldıran bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function removeCharacter($text, $char) {
    return str_replace($char, "", $text);
}

$text = "Bu bir test metni.";
echo removeCharacter($text, " "); // Çıktı: "Bubirtestmetni."
```

---

### **3.45 PHP’de bir metindeki belirli bir karakterin kaç kez tekrarlandığını bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function countCharacter($text, $char) {
    return substr_count($text, $char);
}

$text = "Bu bir test metni.";
echo countCharacter($text, "e"); // Çıktı: 2
```

---

### **3.46 PHP’de bir metindeki belirli bir kelimenin kaç kez tekrarlandığını bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function countWord($text, $word) {
    return substr_count($text, $word);
}

$text = "Bu bir test metni. Bu metin bir test için yazıldı.";
echo countWord($text, "test"); // Çıktı: 2
```

---

### **3.47 PHP’de bir metindeki belirli bir kelimenin pozisyonunu bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function findWordPosition($text, $word) {
    return strpos($text, $word);
}

$text = "Bu bir test metni.";
echo findWordPosition($text, "test"); // Çıktı: 8
```

---

### **3.48 PHP’de bir metindeki belirli bir kelimenin son pozisyonunu bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function findLastWordPosition($text, $word) {
    return strrpos($text, $word);
}

$text = "Bu bir test metni. Bu metin bir test için yazıldı.";
echo findLastWordPosition($text, "test"); // Çıktı: 30
```

---

### **3.49 PHP’de bir metindeki belirli bir kelimenin tüm pozisyonlarını bulan bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function findAllWordPositions($text, $word) {
    $positions = [];
    $offset = 0;
    while (($pos = strpos($text, $word, $offset)) !== false) {
        $positions[] = $pos;
        $offset = $pos + strlen($word);
    }
    return $positions;
}

$text = "Bu bir test metni. Bu metin bir test için yazıldı.";
print_r(findAllWordPositions($text, "test")); // Çıktı: [8, 30]
```

---

### **3.50 PHP’de bir metindeki belirli bir kelimenin etrafına HTML tag’leri ekleyen bir fonksiyon yazınız.**  
✍ **Cevap:**  
```php
function highlightWord($text, $word, $tag = "strong") {
    return preg_replace("/\b$word\b/", "<$tag>$word</$tag>", $text);
}

$text = "Bu bir test metni.";
echo highlightWord($text, "test"); // Çıktı: "Bu bir <strong>test</strong> metni."
```

