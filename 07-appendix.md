# (APPENDIX) Phụ lục {-}

# Một số chứng minh

## Chứng minh Định lý Glivenko--Cantelli
Định lý Glivenko--Cantelli là một trong những kết quả nền tảng của thống kê phi tham số. Một cách chứng minh hiện đại dựa trên bất đẳng thức Dvoretzky--Kiefer--Wolfowitz (DKW).

::: {.proof name="Gợi ý chứng minh"}
Xét hàm phân phối tích lũy thực nghiệm
\[
\widehat{F}_n(x) = \frac{1}{n} \sum_{i=1}^{n} \Ind(X_i \le x).
\]
Ta cần chứng minh rằng
\[
\sup_{x\in\mathbb{R}} \left|\widehat{F}_n(x) - F_X(x)\right| \asto 0.
\]
Ý tưởng chứng minh gồm các bước sau.

1. Với mỗi $x$ cố định, biến ngẫu nhiên $\Ind(X_i \le x)$ có phân phối Bernoulli với kỳ vọng $\E\left[\Ind(X_i\le x)\right] = F_X(x)$.

1. Theo Luật số lớn dạng mạnh (Strong Law of Large Number),
\[
\widehat{F}_n(x) \asto F_X(x),
\]
với mọi $x$ cố định.

1. Kết quả trên mới chỉ cho sự hội tụ tại từng điểm. Để nâng lên thành hội tụ đều trên toàn bộ trục số, ta sử dụng bất đẳng thức Dvoretzky--Kiefer--Wolfowitz:
\[
\Pr\left(\sup_{x \in \R} \left|\widehat{F}_n(x) - F(x)\right| > \varepsilon \right) \le 2 \exp(-2n\varepsilon^2),
\]
với mọi $\varepsilon > 0$.

1. Vì
\[
\sum_{n=1}^{\infty} 2\exp(-2n\varepsilon^2) < +\infty,
\]
nên theo bổ đề Borel--Cantelli,
\[
\sup_{x \in \R}\left|\widehat{F}_n(x) - F_X(x) \right| \asto 0.
\]
Điều này hoàn tất chứng minh định lý.
:::
