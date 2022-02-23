
# Barplot
```
barplot_groups=function(sum,xaxis,yaxis,min,max,title,label,xx,yy,zz) {
  ggplot(sum) +
    geom_bar(aes(x=xx, y=yy, fill=zz), stat="identity", alpha=0.5, width=0.5,position=position_dodge(1)) +
    geom_errorbar(aes(x=xx,ymin=mean-se, ymax=mean+se,group=zz), position=position_dodge(1),width=0.1, size=.7) +
    xlab(xaxis) +
    ylab(yaxis) +
    ggtitle(title)+
    scale_colour_hue(name="Tissue Type", l=40) + 
    scale_x_discrete(labels = label) +
    scale_y_continuous(expand = c(0, 0),limits=c(min,max)) +
    theme_bw() +
    theme(axis.ticks.x = element_blank(),
          axis.title.x = element_blank(),
          axis.text.x   = element_text(size=10, color="black"),
          axis.title.y  = element_text(face="bold", size=12),
          axis.text.y   = element_text(size=10, color="black"),
          legend.background = element_rect(size=0.5, linetype="solid",colour ="black"))
  
}
```
 
```
barplot=function(sum,xaxis,yaxis,min,max,title,label,xx,yy) {
  ggplot(sum) +
    geom_bar(aes(x=xx, y=yy), stat="identity", alpha=0.5,width=0.5, position=position_dodge(1)) +
    geom_errorbar(aes(x=xx,ymin=mean-se, ymax=mean+se), position=position_dodge(1),width=0.1, size=.7) +
    xlab(xaxis) +
    ylab(yaxis) +
    ggtitle(title)+
    scale_colour_hue(name="Tissue Type", l=40) + 
    scale_x_discrete(labels = label) +
    scale_y_continuous(expand = c(0,0 ),limits=c(min,max)) +
    theme_bw() +
    theme(axis.ticks.x = element_blank(),
          axis.title.x = element_blank(),
          axis.text.x   = element_text(size=10, color="black"),
          axis.title.y  = element_text(face="bold", size=12),
          axis.text.y   = element_text(size=10, color="black"),
          legend.background = element_rect(size=0.5, linetype="solid",colour ="black")) 
  
}
```
 
# Boxplot

```
boxplot_groups=function(sum,xaxis,yaxis,title,min,max,lable,xx,yy,zz) { 
  ggplot(sum, aes(x=xx, y=yy,fill=zz)) + geom_boxplot(outlier.shape = NA) +
    coord_cartesian(ylim=c(min,max))+
    xlab(xaxis) +
    ylab(yaxis) +
    ggtitle(title)+
    scale_colour_hue(name="Tissue Type", l=40) + 
    scale_x_discrete(labels = lable) +
    theme_bw() + theme(axis.ticks.x = element_blank(),
                       axis.title.x = element_blank(),
                       axis.text.x   = element_text(size=10, color="black"),
                       axis.title.y  = element_text(face="bold", size=12),
                       axis.text.y   = element_text(size=10, color="black"),
                       legend.background = element_rect(size=0.5, linetype="solid",colour ="black"))
} 
```

```
boxplot=function(sum,xaxis,yaxis,title,min,max,xx,yy) { 
  ggplot(sum, aes(x=xx, y=yy)) + geom_boxplot(outlier.shape = NA) +
    coord_cartesian(ylim=c(min,max))+
    xlab(xaxis) +
    ylab(yaxis) +
    ggtitle(title)+
    scale_colour_hue(name="Tissue Type", l=40) + 
    theme_bw() + theme(axis.ticks.x = element_blank(),
                       axis.title.x = element_blank(),
                       axis.text.x   = element_text(size=10, color="black"),
                       axis.title.y  = element_text(face="bold", size=12),
                       axis.text.y   = element_text(size=10, color="black"),
                       legend.background = element_rect(size=0.5, linetype="solid",colour ="black"))
}
```

# Jitterplot

```
jitterplot=function(sum,xaxis,yaxis,title,min,max,xx,yy) { 
  ggplot(sum, aes(x=xx, y=yy)) + 
    geom_violin(trim=FALSE) +
    geom_jitter(shape=16, position=position_jitter(0.05),size=3) +
    coord_cartesian(ylim=c(min,max))+
    xlab(xaxis) +
    ylab(yaxis) +
    ggtitle(title)+
    scale_colour_hue(name="Tissue Type", l=40) + 
    theme_bw() + theme(axis.ticks.x = element_blank(),
                       axis.title.x = element_blank(),
                       axis.text.x   = element_text(size=10, color="black"),
                       axis.title.y  = element_text(face="bold", size=12),
                       axis.text.y   = element_text(size=10, color="black"),
                       legend.background = element_rect(size=0.5, linetype="solid",colour ="black"))
}
```
