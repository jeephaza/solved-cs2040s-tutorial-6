Download Link: https://assignmentchef.com/product/solved-cs2040s-tutorial-6
<br>
<h1>Problem 1.            The Missing Element</h1>

Let’s revisit the same old problem that we’ve started with since the beginning of the semester, finding missing items in the array. Given <em>n </em>items in no particular order, but this time possibly with duplicates, find the first missing number if we were to start counting from 1, or output “all present” if all values 1 to <em>n </em>were present in the input.

For example, given [8<em>,</em>5<em>,</em>3<em>,</em>3<em>,</em>2<em>,</em>1<em>,</em>5<em>,</em>4<em>,</em>2<em>,</em>3<em>,</em>3<em>,</em>2<em>,</em>1<em>,</em>9], the first missing number here is 6.

<strong>Bonus: </strong>(no need for hash functions): Can we do the same thing using <em>O</em>(1) space? i.e. in-place.

<strong>Problem 2.            Coupon Chaos!</strong>

Mr. Nodle has some coupons that he wishes to spend at his favourite cafe on campus, but there are different types of coupons. In particular, there are <em>t </em>distinct coupons types, and he can have any number of each type (including 0). He has <em>n </em>coupons in total.

He wishes to use one coupon a day, starting from day 1. He wishes to use his coupons in ascending order and will use up all his coupons that are of a lower type first before moving on to the next type. Nodle wishes to build a calendar that will state which coupon he will be using.

<ul>

 <li>The list of coupons will be given in an array. An example of a possible input is: [5<em>,</em>20<em>,</em>5<em>,</em>20<em>,</em>3<em>,</em>20<em>,</em>3<em>,</em>20].</li>

</ul>

Here, <em>t </em>= 3, and <em>n </em>= 8. The output here would be [3<em>,</em>3<em>,</em>5<em>,</em>5<em>,</em>20<em>,</em>20<em>,</em>20<em>,</em>20].

<ul>

 <li>Since the menu at the cafe that he frequents is not very diverse, there aren’t many different types of coupons. So we’ll say that <em>t </em>is much smaller than <em>n</em>.</li>

</ul>

Give as efficient an algorithm as you can, to build his calendar for him.

<h1>Problem 3.            Data Structure 2.0</h1>

Let’s try to improve upon the kind of data structures we’ve been using so far a little. Implement a data structure with the following operations:

<ol>

 <li>Insert in <em>O</em>(log<em>n</em>) time</li>

 <li>Delete in <em>O</em>(log<em>n</em>) time</li>

 <li>Lookup in <em>O</em>(1) time</li>

 <li>Find successor and predecessor in <em>O</em>(1) time</li>

</ol>

<h1>Problem 4.             Locality Sensitive Hashing (Optional)</h1>

So far, we have seen several different uses of hash functions. You can use a hash function to implement a <em>symbol table abstract data type</em>, i.e., a data structure for inserting, deleting, and searching for key/value pairs. You can use a hash function to build a fingerprint table or a Bloom filter to maintain a set. You can also use a hash function as a “signature” to identify a large entity as in a Merkle Tree.

Today we will see yet another use: clustering similar items together. In some ways, this is completely the opposite of a hash table, which tries to put every item in a unique bucket. Here, we want to put similar things together. This is known as <em>Locality Sensitive Hashing</em>. This turns out to be very useful for a wide number of applications, since often you want to be able to easily find items that are similar to each other.

We will start by looking at 1-dimensional and 2-dimensional data points, and then (optionally, if there is time and interest) look at a neat application for a more general problem where you are trying to cluster users based on their preferences.

<strong>Problem 4.a. </strong>For simplicity, assume the type of data you are storing are <em>non-negative integers</em>. If two data points <em>x </em>and <em>y </em>have distance ≤ 1, then we want them to be stored in the same bucket. Conversely, if <em>x </em>and <em>y </em>have distance ≥ 2, then we want them to be stored in different buckets. More precisely, we want a random way to choose a hash function <em>h </em>such that the following two properties hold for every pair of elements <em>x </em>and <em>y </em>in our data set:

<ul>

 <li>If |<em>x </em>− <em>y</em>| ≤ 1, then Pr[<em>h</em>(<em>x</em>) = <em>h</em>(<em>y</em>)] ≥ 2<em>/</em>3. • If |<em>x </em>− <em>y</em>| ≥ 2, then Pr[<em>h</em>(<em>x</em>) 6= <em>h</em>(<em>y</em>)] ≥ 2<em>/</em>3.</li>

</ul>

How should you do this? How big should the buckets be? How should you (randomly) choose the hash function? See if you can show that the strategy has the desired property.

<strong>Problem 4.b. </strong>Now let’s extend this to two dimensions. You can imagine that you are implementing a game that takes place on a 2-dimensional world map, and you want to be able to quickly lookup all the players that are near to each other. For example, in order to render the view of player “Bob”, you might lookup “Bob” in the hash table. Once you know <em>h</em>(“<em>Bob</em><sup>00</sup>), you can find all the other players in the same “bucket” and draw them on the screen.

Extend the technique from the previous part to this 2-dimensional setting. What sort of guarantees

do you want? How do you do this? (There are several possible answers here!)

<strong>Problem 4.c. </strong>What if we don’t have points in Euclidean space, but some more complicated things to compare. Imagine that the world consists of a large number of movies (<em>M</em><sub>1</sub><em>,M</em><sub>2</sub><em>,…,M<sub>k</sub></em>). A user is defined by their favorite movies. For example, my favorite movies are (<em>M</em><sub>73</sub><em>,M</em><sub>92</sub><em>,M</em><sub>124</sub>). Bob’s favorite movies are (<em>M</em><sub>2</sub><em>,M</em><sub>92</sub>).

One interesting question is how do you define distance? How similar or far apart are two users? One common notion looks at what fraction of their favorite movies are the same. This is known as Jacard distance. Assume <em>U</em><sub>1 </sub>is the set of user 1’s favorite movies, and <em>U</em><sub>2 </sub>is the set of user 2’s favorite movies. Then we define the distance as follows:

So taking the example of myself and Bob (above), the intersection of our sets is size 1, i.e., we both like movie <em>M</em><sub>92</sub>. The union of our sets is size 4. So the distance from me to Bob is (1−1<em>/</em>4) = 3<em>/</em>4. It turns out that this is a distance metric, and is quite a useful way to quantify how similar or far apart two sets are.

Now we can define a hash function on a set of preferences. The hash function is defined by a permutation <em>π </em>on the set of all the movies. In fact, choose <em>π </em>to be a random permutation. That is, we are ordering all the movies in a random fashion. Now we can define the hash function:

<em>h<sub>π</sub></em>(<em>U</em>) = min(<em>π</em>[<em>j</em>] ∈ <em>U</em>) <em>j</em>

The hash function returns the index of the first movie encountered in permutation <em>π </em>that is also in the set of favourite movies <em>U</em>. For example, if <em>π </em>is {<em>M</em><sub>43</sub><em>,M</em><sub>92</sub><em>,…,M</em><sub>124</sub><em>,…,M</em><sub>73</sub><em>,…</em>} and <em>U </em>= {<em>M</em><sub>73</sub><em>,M</em><sub>92</sub><em>,M</em><sub>124</sub>}, <em>h<sub>π</sub></em>(<em>U</em>) will give 1 as it maps to the index of <em>M</em><sub>92 </sub>in <em>π</em>.

This turns out to be a pretty useful hash function: it is known as a MinHash. One useful property of a MinHash is that it maps two similar users to the same bucket. Prove the following: for any two users <em>U</em><sub>1 </sub>and <em>U</em><sub>2</sub>, if <em>π </em>is chosen as a uniformly random permutation, then:

Pr[<em>h<sub>π</sub></em>(<em>U</em><sub>1</sub>) = <em>h<sub>π</sub></em>(<em>U</em><sub>2</sub>)] = 1 − <em>d</em>(<em>U</em><sub>1</sub><em>,U</em><sub>2</sub>)

The closer the are, they more likely they are in the same bucket! The further apart, the more likely they are in different buckets.

<h1>Problem 5.               Optional Reading: Learned Bloom Filters</h1>

There is always a possibility of a false positive when non-member objects coincidentally map to set bit positions in the bloom filter array, but can we improve the bloom filter in terms of space while achieving the same false positive probability through the use of machine learning? Read more about it here: