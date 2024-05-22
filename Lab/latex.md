## `Latex`

>[`Latex`和`vscode`环境搭建](https://www.bilibili.com/video/BV1ht4y197Nz/?spm_id_from=333.788.top_right_bar_window_history.content.click&vd_source=81d07727a431bd6b2d07b94e67a294fc)
>
>[知乎 `Latex`推荐文章](https://www.zhihu.com/question/24676172)
>
>[一个非常快速的 Latex 入门教程](https://www.bilibili.com/video/BV11h41127FD/?spm_id_from=333.337.search-card.all.click&vd_source=81d07727a431bd6b2d07b94e67a294fc)

## 字体大小格式

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
\ctexset {
    part/pagestyle = empty,
    chapter = {
        format = \raggedright,
        pagestyle = empty,
    },
    section = {
        name = {,、},
        number = \chinese{section},
    }
}

% 导言区
\usepackage{amsmath}
\usepackage{graphicx}

% 自定义命令
\newcommand\infoTitle[1]{\title{\zihao{1}{#1}}} 
\newcommand\info[4]{
\begin{center} \Large
    \begin{tabular}{rl}
        % after \\: \hline or \cline{col1-col2} \cline{col3-col4} ...
        题目名称: & \underline{\makebox[10cm][l]{#1}} \\ 
        学生学号: & \underline{\makebox[10cm][l]{#2}} \\ 
        学生姓名: & \underline{\makebox[10cm][l]{#3}} \\ 
        指导教师: & \underline{\makebox[10cm][l]{#4}} \\ 
    \end{tabular}
\end{center}}

\infoTitle{《图像处理与科学计算》课程大作业}

\begin{document}
\maketitle
% 此处分别填入 题目名称 学生学号 学生姓名 指导教师
\info{图像处理与科学计算的应用}{2021201517}{陈威翰}{刘咏梅}

\newpage

\tableofcontents
\newpage

\section{问题背景}
% 在此部分填写问题背景的内容

\section{国内外研究现状}

\subsection{国内研究现状}
% 在此部分填写国内研究现状的内容

\subsection{国外研究现状}
% 在此部分填写国外研究现状的内容

\section{原理、方法、技术介绍}

\subsection{相关原理}
% 在此部分填写相关原理的内容

\subsection{研究方法}
% 在此部分填写研究方法的内容

\section{基于***的***方法}
% 在此部分填写基于某种技术的方法的内容

\section{结论}
% 在此部分填写结论的内容

\section{参考文献}
% 在此部分填写参考文献
%\bibliography{text}

\appendix

\section{源代码}
% 在此部分添加源代码

\end{document}

```

