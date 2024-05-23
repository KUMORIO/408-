## `Latex`

>[`Latex`和`vscode`环境搭建](https://www.bilibili.com/video/BV1ht4y197Nz/?spm_id_from=333.788.top_right_bar_window_history.content.click&vd_source=81d07727a431bd6b2d07b94e67a294fc)
>
>[知乎 `Latex`推荐文章](https://www.zhihu.com/question/24676172)
>
>[一个非常快速的 Latex 入门教程](https://www.bilibili.com/video/BV11h41127FD/?spm_id_from=333.337.search-card.all.click&vd_source=81d07727a431bd6b2d07b94e67a294fc)

## 字体大小格式

https://blog.csdn.net/Raging__Fire/article/details/115021175

>在 LaTeX 中，还有其他一些字体大小命令，例如：
>
>- `\tiny`: 最小的字体大小。
>- `\small`: 小号字体。
>- `\normalsize`: 默认的正常大小字体。
>- `\large`: 比 `\normalsize` 大一些的字体。
>- `\LARGE`: 比 `\large` 大一些的字体。
>- `\Huge`: 比 `\LARGE` 大一些的字体。
>
>这些命令提供了一系列不同大小的选项，你可以根据需要选择适合的字体大小。

图像处理latex模板

```la
\documentclass[UTF8]{ctexart}
%导言区

\usepackage{amsmath}
\usepackage{graphicx}
\ctexset {
    section = {
        name = {,、},
        number = \chinese{section},
    }
}
%自定义命令
\newcommand\infoTitle[2]{\title{\zihao{1}{#1} \\ \zihao{1}{#2}}}
\newcommand\info[4]{
\begin{center} \Large
	\begin{tabular}{rl}
		% after \\: \hline or \cline{col1-col2} \cline{col3-col4} ...
		题目名称: & #1 \\
		学生学号: & #2 \\
		学生姓名: & #3 \\
		% \quad \\
    指导教师: & #4 \\
		% 姓名: & #5 \\
	\end{tabular}
\end{center}}

\infoTitle{《图像处理与科学计算》课程}{大作业}

%\bibliographystyle{plain}
\begin{document}
\date{}
\maketitle
%此处分别填入  课程名称   课程性质（选修或必修）     实验题目    姓名   学号
\info{111}{2021201517}{陈威翰}{刘咏梅}%{学号}

\newpage
\tableofcontents
\newpage
\section{实验目的}
                                               
\section{实验要求及实验环境}

\subsection{实验要求}

\subsection{实验环境}


\section{设计思想}

\subsection{算法原理}

\subsection{算法的实现}

\section{实验结果与分析}


\section{结论}


\section{参考文献}
%\bibliography{text}
\appendix

\section{源代码}
\end{document}
```

>论文引用
>
>[1] P. Oberdiek, M. Rottmann, and H. Gottschalk, “Classification uncertainty of deep neural networks based
>on gradient information,” CoRR, vol. abs/1805.08440,
>2018.
>[2] K. Lee, K. Lee, H. Lee, and J. Shin, “A simple uni-
>fied framework for detecting out-of-distribution samples and adversarial attacks,” in Advances in Neural
>Information Processing Systems 31, 2018, pp. 7167–
>7177.
>[3] Y. Bahat and G. Shakhnarovich, “Confidence from
>invariance to image transformations,” ArXiv, vol.
>abs/1804.00657, 2018.
>[4] H. Jiang, B. Kim, M. Guan, and M. Gupta, “To trust or
>not to trust a classifier,” in Advances in Neural Information Processing Systems 31, 2018, pp. 5541–5552.
>
>[5] S. Liu, R. Garrepalli, T. G. Dietterich, A. Fern, and
>D. Hendrycks, “Open category detection with PAC
>guarantees,” CoRR, vol. abs/1808.00529, 2018.
>[6] J. Ren, P. J. Liu, E. Fertig, J. Snoek, R. Poplin, M. A.
>DePristo, J. V. Dillon, and B. Lakshminarayanan,
>“Likelihood ratios for out-of-distribution detection,”
>ArXiv, vol. abs/1906.02845, 2019.
>[7] Q. Yu and K. Aizawa, “Unsupervised out-ofdistribution detection by maximum classifier discrepancy,” in Proceedings of the IEEE International Conference on Computer Vision, 2019, pp. 9518–9526.
>
>[8] S. Liang, Y. Li, and R. Srikant, “Enhancing the reliability of out-of-distribution image detection in neural networks,” in International Conference on Learning Representations, 2018.
>[9] W. Lawson, E. Bekele, and K. Sullivan, “Finding
>anomalies with generative adversarial networks for a
>patrolbot,” in 2017 IEEE Conference on Computer Vision and Pattern Recognition Workshops (CVPRW),
>July 2017, pp. 484–485.
>[10] X. W. Wenhu Chen, Yilin Shen and W. Wang, “Enhancing the robustness of prior network in out-ofdistribution detection,” CoRR, vol. abs/1811.07308,
>2018.
>[11] I. Golan and R. El-Yaniv, “Deep anomaly detection using geometric transformations,” in Advances in Neural Information Processing Systems, 2018, pp. 9758–
>9769.
>[12] T. Denouden, R. Salay, K. Czarnecki, V. Abdelzad,
>B. Phan, and S. Vernekar, “Improving reconstruction
>autoencoder out-of-distribution detection with mahalanobis distance,” ArXiv, vol. abs/1812.02765, 2018.
>[13] P. Schulam and S. Saria, “Can you trust this prediction?
>auditing pointwise reliability after learning,” in Proceedings of Machine Learning Research, ser. Proceedings of Machine Learning Research, vol. 89. PMLR,
>16–18 Apr 2019, pp. 1022–1031.
>
>[14] J. H. Metzen, T. Genewein, V. Fischer, and
>B. Bischoff, “On detecting adversarial perturbations,”
>arXiv preprint arXiv:1702.04267, 2017.
>[15] R. Feinman, R. R. Curtin, S. Shintre, and A. B. Gardner, “Detecting adversarial samples from artifacts,”
>ArXiv, vol. abs/1703.00410, 2017.
>[16] F. Carrara, R. Becarelli, R. Caldelli, F. Falchi, and
>G. Amato, “Adversarial examples detection in features
>distance spaces,” in Proceedings of the European Conference on Computer Vision (ECCV), 2018.
>[17] X. Ma, B. Li, Y. Wang, S. M. Erfani, S. Wijewickrema, G. Schoenebeck, D. Song, M. E. Houle,
>and J. Bailey, “Characterizing adversarial subspaces
>using local intrinsic dimensionality,” arXiv preprint
>arXiv:1801.02613, 2018.
>
>[18] Y. Song, T. Kim, S. Nowozin, S. Ermon, and N. Kushman, “Pixeldefend: Leveraging generative models to
>understand and defend against adversarial examples,”
>CoRR, vol. abs/1710.10766, 2017.
>[19] D. Miller, Y. Wang, and G. Kesidis, “When not to classify: Anomaly detection of attacks (ADA) on DNN
>classifiers at test time,” Neural Computation, 12 2017.
>[20] F. Carrara, F. Falchi, R. Caldelli, G. Amato, R. Fumarola, and R. Becarelli, “Detecting adversarial example attacks to deep neural networks,” in Proceedings
>of the 15th International Workshop on Content-Based
>Multimedia Indexing. ACM, 2017, p. 38.

