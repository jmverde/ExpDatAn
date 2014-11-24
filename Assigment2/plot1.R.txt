plot1<-function(){
    
    ## Have total emissions from PM2.5 decreased in the United States from 1999 to
    ## 2008? Using the base plotting system, make a plot showing the total PM2.5
    ## emission from all sources for each of the years 1999, 2002, 2005, and 2008.
    
    
    
    ## Loading data
    NEI <- readRDS("./data/summarySCC_PM25.rds")
    SCC <- readRDS("./data/Source_Classification_Code.rds")
 
    # We need the emissions splited per year
    groups<-split(NEI$Emissions,NEI$year)
    
    # We sum the emisions in every source
    res<-sapply(groups,sum)
    
    # Create a dataframe to ease work 
    
    datagraph<-as.data.frame(res)
    datagraph$year<-rownames(datagraph)
    rownames(datagraph)<-1:nrow(datagraph)
    
    png(file="plot1.png",480,480)
    
    with(datagraph,plot(year,res,
                        xlab ="Year",
                        ylab = expression('Tons of PM'[2.5]*'  emitted'),
                        main = expression("Total emissions from PM "[2.5]*" in the U.S. from 1999 to 2008")))
    
    
    
    dev.off()
    
}