# Linear Model functions

```r
beta <- function(x,y,model=NULL){
  if(is.null(model)){
    return(solve(t(x)%*%x)%*%t(x)%*%y)
  } else if(model=="a"){ # ANOVA
    return(Ginv(t(x)%*%x)%*%t(x)%*%y)
    
  }
}
sse <- function(x,y,b){
  return(t(y)%*%y-t(b)%*%t(x)%*%y)
}
ssr <- function(x,y,b){
  return(t(b)%*%t(x)%*%y-nrow(x)%*%mean(y)^2)
}
sst <- function(x,y){
  return(t(y)%*%y-nrow(x)%*%mean(y)^2)  
}
ss <- function(b,bs,x,xs,y){
  return(t(b)%*%t(x)%*%y - t(bs)%*%t(xs)%*%y)
}
ssh <- function(c,b,x){
  return(t(c%*%b)%*%solve(c%*%solve(t(x)%*%x)%*%t(c))%*%c%*%b)
}
ti <- function(b_j,s,g_jj){
  t_i <- b_j/(s%*%sqrt(g_jj))
  p_val <- 2-2*pt(gas.t1, 27, lower.tail = F)
  return(cat('t:',round(t_i,3),'p-val:',round(p_val,3)))
}
ci <- function(x,b,s,g,p,k){
  lower <- b-qt(p,nrow(x)-k-1,lower.tail = F)%*%s%*%sqrt(g)
  upper <- b+qt(p,nrow(x)-k-1,lower.tail = F)%*%s%*%sqrt(g)
  return(paste0(round(lower,3),',',round(upper,3)))
}
ci.e <- function(x,x0,b,s,g,p,k){
  lower <- x0%*%b-qt(p,nrow(x)-k-1,lower.tail = F)%*%s%*%sqrt(t(x0)%*%g%*%x0)
  upper <- x0%*%b+qt(p,nrow(x)-k-1,lower.tail = F)%*%s%*%sqrt(t(x0)%*%g%*%x0)
  return(paste0(round(lower,3),',',round(upper,3)))
}
ci.p <- function(x,x0,b,s,g,p,k){
  lower <- x0%*%b-qt(p,nrow(x)-k-1,lower.tail = F)%*%s%*%sqrt(1+t(x0)%*%g%*%x0)
  upper <- x0%*%b+qt(p,nrow(x)-k-1,lower.tail = F)%*%s%*%sqrt(1+t(x0)%*%g%*%x0)
  return(paste0(round(lower,3),',',round(upper,3)))
}
fs <- function(nu,de,num,h,k){
  f_test <- (nu/h)/(de/(num-k-1))
  f_pval <- pf(f_test,h,num-k-1, lower.tail=F)
  return(cat('F:',round(f_test,3),'p-val:',round(f_pval,3)))
}

```
