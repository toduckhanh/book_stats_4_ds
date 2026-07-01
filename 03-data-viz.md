# Trực quan hóa dữ liệu

## Sự liên hệ giữa dữ liệu và biến ngẫu nhiên

### Dữ liệu và biến ngẫu nhiên


::: {.remark #sample }
Ta thống nhất các ký hiệu sau:

- **Mẫu ngẫu nhiên** (**random sample**): $X_1, \ldots, X_n$ là các biến ngẫu nhiên độc lập và cùng phân phối (independent and identically distributed - iid).
- **Dữ liệu quan sát** (**observed data**): $x_1, \ldots, x_n$ là các giá trị thu được từ mẫu ngẫu nhiên.
- **Bộ dữ liệu** (**dataset**): tập hợp dữ liệu được lưu trữ để phân tích, có thể gồm nhiều biến, nhiều bảng hoặc nhiều kiểu dữ liệu khác nhau. 

:::


### Sự chuyển đổi biến


## Ước lượng các đặc trưng của dữ liệu
Trong phần này, ta nghiên cứu các ước lượng của các đặc trưng của một biến ngẫu nhiên $X$ dựa trên một mẫu ngẫu nhiên, $X_1, \ldots, X_n$, gồm $n$ biến ngẫu nhiên độc lập và cùng phân phối theo hàm phân phối $F_{X}(x)$. Ta thường viết tắt bởi $X_i \stackrel{\rm iid}{\sim} F_{X}(x)$, với $i = 1, \ldots, n$.


### Phân phối thực nghiệm
Nhắc lại rằng mẫu ngẫu nhiên là một tập hợp các đơn vị thống kê được chọn từ quần thể và kỳ vọng có tính đại diện cho quần thể đó. Do đó, mặc dù phân phối lý thuyết của quần thể hay của biến ngẫu nhiên $X$ thường chưa biết, ta có thể sử dụng các giá trị quan sát của mẫu để xây dựng phân phối thực nghiệm (**empirical distribution**), từ đó suy luận về phân phối của quần thể.

::: {.definition #ecdf name="Phân phối thực nghiệm"}
Xét một mẫu ngẫu nhiên $X_1, \ldots, X_n$, độc lập và cùng phân phối của biến ngẫu nhiên $X$ có hàm phân phối tích lũy $F_X(x) = \Pr(X \le x)$. Hàm phân phối tích lũy thực nghiệm (**empirical cumulative distribution** - ECDF) của $X$ được xác định bởi
\begin{equation}
\widehat{F}_n(x) = \frac{1}{n}\sum_{i = 1}^{n} \Ind\left(X_i \le x\right),
(\#eq:ecdf)
\end{equation}
là một ước lượng của $F_X$, với $\Ind(\cdot)$ là hàm chỉ (indicator function) và được định nghĩa như sau:
\[
\Ind\left(u \le a\right) = \begin{cases}
1 & \text{ nếu } u \le a, \\
0 & \text{ nếu } u > a.
\end{cases}
\]
:::

Hàm phân phối tích lũy thực nghiệm trong phương trình \@ref(eq:ecdf) là một trong những công cụ cơ bản và lâu đời nhất của thống kê phi tham số. Ý tưởng xây dựng ECDF xuất phát từ việc thay thế phân phối lý thuyết chưa biết của quần thể bằng tần suất tích lũy quan sát được từ mẫu. Mặc dù khái niệm này đã xuất hiện từ rất sớm trong thống kê toán học, nền tảng lý thuyết của ECDF được thiết lập rõ ràng thông qua định lý Glivenko--Cantelli, chứng minh rằng hàm phân phối thực nghiệm hội tụ đều đến hàm phân phối thực của quần thể khi cỡ mẫu lớn [@Glivenko1933; @Cantelli1933]. Kể từ đó, ECDF trở thành nền tảng của nhiều phương pháp thống kê phi tham số, bao gồm kiểm định Kolmogorov--Smirnov, kiểm định Cramér--von Mises, ước lượng phân vị và các kỹ thuật bootstrap hiện đại [@vanDerVaart1998; @Wasserman2004].


::: {.theorem #gliv name="Định lý Glivenko--Cantelli"}
Xét một mẫu ngẫu nhiên $X_1, \ldots, X_n$, độc lập và cùng phân phối của biến ngẫu nhiên $X$ có hàm phân phối tích lũy $F_X(x)$. Ký hiệu $\widehat{F}_n(x)$ là hàm phân phối tích lũy thực nghiệm được xây dựng từ mẫu ngẫu nhiên. Khi đó,
\[
\sup_{x\in\mathbb{R}} \left|\widehat{F}_n(x) - F_X(x) \right| \asto 0,
\]
khi $n \to +\infty$.
:::

[[Bổ sung chứng minh trong phụ lục.]]

Từ định lý Glivenko-Cantelli ta có kết quả quan trọng sau cho việc ước lượng phân phối tích lũy tại một giá trị cố định.

::: {.corollary #ecdf-consistency}
Với mọi $x \in \R$,
\[
\widehat{F}_n(x) \asto F_X(x),
\]
khi $n \to +\infty$. Do đó, ta nói $\widehat{F}_n(x)$ là một ước lượng vững của $F_X(x)$.
:::

### Ước lượng mật độ xác suất
Hàm mật độ xác suất của biến ngẫu nhiên ngoài công dụng trong việc xác định xác suất tích lũy, thì nó cũng biểu diễn sự phân bố của giá trị lý thuyết của biến ngẫu nhiên, trong đó, vùng có giá trị mật độ xác suất cao nhất thì tương ứng với vùng có khả cao có thể quan sát được giá trị của biến ngẫu nhiên.

Trong phần trước, ta đã được giới thiệu tới hàm phân phối tích lũy thực nghiệm $\widehat{F}_n(x)$, từ hàm này, ta hoàn toàn có thể xác định được hàm mật độ xác suất cho mẫu ngẫu nhiên. Nhắc lại rằng, hàm mật độ xác suất lý thuyết của một biến ngẫu nhiên liên tục $X$, được ký hiệu là $f_X(x)$ và được xác định bởi 
$$f_X(x) = \dfrac{\ud}{\ud x} F_X(x)$$,
tức là đạo hàm của hàm phân phối tích lũy lý thuyết $F_X(x)$.

Xét một mẫu ngẫu nhiên $X_1, \ldots, X_n$, độc lập và cùng phân phối của biến ngẫu nhiên $X$ có hàm phân phối tích lũy $F_X(x)$ và hàm mật độ xác suất $f_X(x)$ (chưa biết). Hàm xác suất tích lũy thực nghiệm $\widehat{F}_n(x)$ trong \@ref(eq:ecdf) là ước lượng của $F_X(x)$. Ta mong muốn ước lượng được hàm mật độ xác suất $f_X(x)$ dựa trên mẫu ngẫu nhiên. Áp dụng định nghĩa của hàm mật độ xác suất, ta có thể viết
\[
\widehat{f}_n(x) = \dfrac{\ud}{\ud x} \widehat{F}_n(x).
\]
Tuy nhiên $\widehat{F}_n(x)$ là không liên tục, do đó ta cần áp dụng xấp xỉ sai phân trung tâm (central difference approximation) với bước nhảy $h > 0$, khi này, ta có 
\begin{eqnarray}
\widehat{f}_n(x) &=& \dfrac{\widehat{F}_n(x + h/2) - \widehat{F}_n(x - h/2)}{h} \nonumber \\
&=& \frac{1}{nh}\sum_{i = 1}^{n} \mathrm{I}\left(\frac{|Y_i - x|}{h} \le \frac{1}{2}\right) (\#eq:dens-hist).
\end{eqnarray}
Ước lượng này được gọi là ước lượng mật độ tần số thực nghiệm (the histogram estimator) được đề xuất và nghiên cứu các tính chất thống kê bởi @freedman1981histogram. Tham số $h$ được gọi là ``độ rộng'' (bandwidth). Ta dễ dàng kiểm chứng được các tính chất cho $\widehat{f}_n(x)$ (xem thêm trong phụ lục ...). 


Không giống như hàm phân phối tích lũy thực nghiệm, hàm mật độ tần số thực nghiệm bị ảnh hưởng bởi việc lựa chọn độ rộng $h$. Khi $h$ càng nhỏ ($h \to 0$) thì hàm mật độ tần số thực nghiệm sẽ càng gấp khúc, trong khi giá trị lớn của $h$ tạo ra ước lượng mật độ có vẻ trơn, tuy nhiên, nếu $h$ quá lớn thì tính chính xác của ước lượng không còn được đảm bảo. @freedman1981histogram đề xuất một cách chọn $h$ ``tối ưu'' là $h_{\mathrm{opt}, \mathrm{FD}} = 2 \mathrm{IQR} n^{-1/3}$.


### Trung bình mẫu và phương sai mẫu


### Phân vị mẫu






## Trực quan dữ liệu bởi số tổng hợp


## Trực quan dữ liệu bởi biểu đồ

### Biểu đồ stem-leaf

### Biểu đồ điểm

### Biểu đồ histogram

### Biểu đồ boxplot

### Biểu đồ mật độ xác suất


## Trực quan mối liên hệ trong dữ liệu

### Biểu đồ side-by-side boxplot

### Hệ số tương quan





