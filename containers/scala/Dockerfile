FROM java

#Scala
RUN apt-get remove scala-library scala
RUN wget http://www.scala-lang.org/files/archive/scala-2.11.4.deb
RUN dpkg -i scala-2.11.4.deb
RUN apt-get update
RUN apt-get install scala
 
# sbt installation
# remove sbt:>  sudo apt-get purge sbt.
 
RUN wget http://dl.bintray.com/sbt/debian/sbt-0.13.6.deb
RUN dpkg -i sbt-0.13.6.deb 
RUN apt-get update
RUN apt-get install sbt