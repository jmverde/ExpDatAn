plot2<-function(){
    
    
    #The question to solve is Have total emissions from PM2.5 decreased in the
    #Baltimore City, Maryland (fips == "24510") from 1999 to 2008? Use the base
    #plotting system to make a plot answering this question.
    
    ## Loading data
    NEI <- readRDS("./data/summarySCC_PM25.rds")
    SCC <- readRDS("./data/Source_Classification_Code.rds")
    
    ## select only data for Baltimore
    data<-subset(NEI,fips=="24510",select = c(Emissions,year))

    # We need the emissions splited per year
    groups<-split(data$Emissions,data$year)
    
    # We sum the emisions in every source
    res<-sapply(groups,sum)
    
    # Create a dataframe to ease work 
    
    datagraph<-as.data.frame(res)
    datagraph$year<-rownames(datagraph)
    rownames(datagraph)<-1:nrow(datagraph)
    
    png(file="plot2.png",480,480)
    
    with(datagraph,plot(year,res,
                        xlab ="Year",
                        ylab = expression('Tons of PM'[2.5]*'  emitted'),
                        main = expression("Total emissions from PM "[2.5]*" in Baltimore from 1999 to 2008")))
    
    
    dev.off()

         
}