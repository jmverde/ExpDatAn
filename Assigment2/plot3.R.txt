plot3<-function(){
 
   
    ## Loading data
    NEI <- readRDS("./data/summarySCC_PM25.rds")
    SCC <- readRDS("./data/Source_Classification_Code.rds")
    
    ## select only data for Baltimore
    data<-subset(NEI,fips=="24510",select = c(Emissions,year,type))

    ### sumaryce data using ddply 
    
    library(plyr)
    
    summ<-ddply(data,.(type,year),summarise,sum=sum(Emissions))
    
    #Finally construct the plot
    
    library(ggplot2)

    png(file="plot3.png",600,480)
    
   print( qplot(year,sum,data=summ,facets=.~type,geom=c("point","smooth"),
          ylab=expression('Tons of PM'[2.5]*'  emitted')))
    
    dev.off()
    
}