#Extract files with Apache Commons Compress, from any archive

##build.sbt
```scala
libraryDependencies += "org.apache.commons" % "commons-compress" % "1.10"
```

##Unarchive.scala
```scala
package com.ebiznext.utils

import java.io._

import org.apache.commons.compress.archivers.{ArchiveEntry, ArchiveStreamFactory, ArchiveInputStream}
import org.apache.commons.compress.compressors.CompressorStreamFactory
import org.apache.commons.compress.utils.IOUtils

import scala.util.{Failure, Success, Try}

/**
  *
  * Created by smanciot on 29/02/16.
  */
object Unarchive {

  def uncompress(input: BufferedInputStream): InputStream =
    Try(new CompressorStreamFactory().createCompressorInputStream(input)) match {
      case Success(i) => new BufferedInputStream(i)
      case Failure(_) => input
    }

  def extract(input: InputStream): ArchiveInputStream =
    new ArchiveStreamFactory().createArchiveInputStream(input)


  def unarchive(archive: File, directory: File): Long = {
    var nbEntries = 0
    if(archive.isFile && directory.exists()){
      val input = extract(uncompress(new BufferedInputStream(new FileInputStream(archive))))
      def stream: Stream[ArchiveEntry] = input.getNextEntry match {
        case null  => Stream.empty
        case entry => entry #:: stream
      }
      for(entry <- stream) {
        val file = new File(directory, entry.getName)
        if (entry.isDirectory){
          file.mkdirs()
        }
        else{
          val output = new FileOutputStream(file)
          IOUtils.copy(input, output)
          output.close()
          nbEntries = nbEntries + 1
        }
      }
      input.close()
    }
    nbEntries
  }

}
```
