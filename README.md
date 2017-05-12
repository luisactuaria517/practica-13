# practica-13
asa <- read.csv("C:\\Users\\Sala-D11\\Downloads\\asala.csv")


asa <- t(data.frame(read.csv("C:\\Users\\Sala-D11\\Downloads\\asala.csv", header=T)[7, 2:49]))##renglon 7 columna 2 a 49
View(asa)

asa<-as.numeric(asa)
asat<-ts(asa, start=2005, frequency = 4)##para transponer
asat

###suavizado exponencial en R
installed.packages("forecast")
require(forecast)
mod1<-ses(asat, alpha = .1, initial="simple", h=8) ##alpha parametro para suavizar, h=periodos
mod2<-ses(asat, alpha = .3, initial="simple", h=8)
mod3<-ses(asat, alpha = .95,initial="simple", h=8)

x11()#abre una ventana en esta va a graficar
##graficar los valors observados
##mod1 me dara los valores ajustados, que son los que generean en base a alpha .1
##mean es el pronostico
windows()
plot(mod1, ylab="asalariados", xlab = "Año", main="Asalariados", type="o")##2005 a 2016 con alfa .1
lines(mod1$fitted, col="brown", type="o")
lines(mod2$fitted, col="red", type="o")##ya muestra los altos que quiereo
lines(mod3$fitted, col="green", type="o")##ya se parecen a los datos observados"es el que usaria xq estara mas proximo"
lines(mod1$mean, col="brown", type="o")
lines(mod2$mean, col="red", type="o")
lines(mod3$mean, col="green", type="o")
legend("topleft",  lty = 1,col = c(1, "blue", "red", "green"), 
       c("datos", expression(alpha==.1), expression(alpha==.3),
         expression(alpha==.95)), pch=15)##pch cambia el simbolo de nombre de datos
