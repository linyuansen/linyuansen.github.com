---
layout: post
title: "ProjectEuler Problem1 multiples of 3 and 5"
description: ""
category: coding
tags: [lisp, ProjectEuler]
---
{% include JB/setup %}

- Multiples of 3 and 5
--Problem 1
---If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

---Find the sum of all the multiples of 3 or 5 below 1000.

{% highlight cl linenos%}
(defun 2->1list(alist)
  ;(mapcan (lambda(n)(if t n)) alist))
  (if (not (null alist))
      (append (car alist) (2->1list (cdr alist)))))

(defun print-a35 (a b)
  (let ((n1 (* a 3))
	(n2 (* a 5)))
    (if (< n2 b)
	(list n1 n2)
	(if (< n1 b) (list n1)))))

(defun test(a b)
  (if (> a b)
      nil
      (append (print-a35 a b)
	     (test (1+ a) b))))



(defun sort-delete (alist)
  (if (not (null (cadr alist)))	   
      (let ((point-b (car alist))
	    (point-a (cadr alist)))
        (append (if (= point-a point-b) nil (list point-a))
		(sort-delete (cdr alist))))))

(defun sum-list (alist)
  (if (null alist)
      0
      (+ (car alist)
	 (sum-list (cdr alist)))))

;a*3 a*5 1~1000
(defun test-end()
  (let ((alist1 (test 1 1000)));a*3 a*5
    (setq alist1 (sort alist1 #'<));sort <
    (setq alist1 (cons (car alist1);delete repeat
		       (sort-delete alist1)))
    (sum-list alist1)))

(defun test-answer()
  (let ((sum 0))	
    (loop for i from 1 to 999
	 do
	  (if (or
	      (= 0 (mod i 3))
	      (= 0 (mod i 5)))
	     (setq sum (+ sum i))))
    sum))

{% endhighlight %}