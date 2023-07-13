# ToxcodanGenomeFigures
Repository containing the input files and code to generate the figures in ToxCodAn-Genome manuscript.

To plot the barplots and boxplots, just run the R command below for each dataset:
 - In the example it will blor the chart for *Bothrops jararaca* (Bjar).

```R
library(ggplot2)
library(gridExtra)

dataset <- "Bjar"
species <- "Bothrops jararaca"

df <- read.table(paste(dataset, "_number.txt"), header=TRUE, sep = "\t")

B <- ggplot(df, aes(fill=Annotation, y=Number, x=DS)) +
  geom_bar(position="stack", stat="identity", color="black", width=0.5) +
  scale_fill_manual(values = c("forestgreen", "green3"), name = "Annotation") +
  scale_x_discrete(limits = c("TR", "DBTR", "DB", "Genome")) +
  ggtitle(species) + xlab("") + ylab("# of annotated toxins") +
  coord_flip() +
  theme_classic()

ratio <- read.table(paste(dataset, "_ratio.txt"), header=TRUE, sep = "\t")

R <- ggplot(ratio, aes(x=DS, y=ratio)) +
    geom_boxplot(width=0.5, outlier.colour="grey", color="black", fill="grey") +
    geom_dotplot(aes(fill=Toxin), binaxis='y', stackdir='center', position=position_dodge(0.6), dotsize=0.5) +
    geom_hline(yintercept=1, linetype="dashed", color = "grey20", size=0.5) +
    ylim(0, 2) +
    scale_x_discrete(limits = c("TR", "DBTR", "DB", "Genome")) +
    ggtitle(species) + xlab("") + ylab("recovery ratio") +
    coord_flip() +
    theme_classic()

grid.arrange(B, R, ncol=2, nrow=1)
```
