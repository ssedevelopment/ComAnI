# ComAnI
![Build Status](https://jenkins-2.sse.uni-hildesheim.de/buildStatus/icon?job=OSS_Analysis_ComAnI "Build Status")


The Commit Analysis Infrastructure (ComAnI) is an open and configurable infrastructure for the extraction and analysis of commits from software repositories. For both tasks, individual plug-ins realize different extraction and analysis capabilities, which rely on the same data model provided by the infrastructure. Hence, any combination of extraction and analysis plug-ins is possible.
![ComAnI Overview](/guide/inserts/comani_overview.png "ComAnI Overview")
ComAnI enables conducting an analysis for a software hosted in a Git repository first and later conducting the same analysis for a different software hosted by SVN (assuming that the analysis is able to cope with the artifacts and their technologies of the new software under analysis). Another example is to use the same commit extractor, e.g., supporting the commit extraction from Git repositories, for different analyses. The definition of a particular ComAnI instance consists of a set of configuration parameters saved in a configuration file, which the infrastructure reads at start-up. Hence, there is no implementation effort needed. The infrastructure automatically performs its internal setup, loads and starts the desired plug-ins.

The [ComAnI Guide](/guide/ComAnI_Guide.pdf) provides more information about the capabilities of the infrastructure. Note that this guide is currently incomplete and will be updated in future to cover all aspects of the infrastructure.

## Installation
Download the desired Jar from jenkins and save it to a directory of your choice on your machine.

- This project (without sources): ComAnI.jar [ComAnI.jar](https://jenkins-2.sse.uni-hildesheim.de/job/OSS_Analysis_ComAnI/lastSuccessfulBuild/net.ssehub.comani$comani-structure/)
- The whole project with plugins (without sources): [Archive.zip](https://jenkins-2.sse.uni-hildesheim.de/job/OSS_Analysis_ComAniFull/lastSuccessfulBuild/artifact/*zip*/archive.zip)

*Requirements:*
- Java 8 or higher (or equivalents, like OpenJDK)

## Execution
The infrastructure can be executed as a typical Java Jar-file, which expects the following parameters:
- Mandatory: A configuration (properties) file, which defines the particular ComAnI instance and its setup. The available configuration options and their valid values are described in the [ComAnI Guide](/guide/ComAnI_Guide.pdf).
- Optional: the `-i` option can be used to perform a single commit extraction. It has to be followed by the commit information, which is terminated by a last line containing the string “!q!”.

*Examples:*

`java -jar ComAnI.jar /path/to/configuration-file.properties`

or

`java -jar ComAnI.jar /path/to/configuration-file.properties –i <CommitContent>\n!q!`

## Plugins

The following table lists commonly used plugins for ComAnI.
<table style="width:100%">
  <tr>
    <th>Plugin</th>
    <th>Type</th>
    <th>License</th>
    <th>Download</th>
    <th>Status</th>
  </tr>
  <!-- GitCommitExtractor -->
  <tr>
    <td><a href="https://github.com/CommitAnalysisInfrastructure/GitCommitExtractor">GitCommitExtractor</a></td>
    <td><b>Commit-Extractor:</b> Extract commits from git repositories</td>
    <td><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache License 2.0</a></td>
    <td><a href="https://jenkins-2.sse.uni-hildesheim.de/job/OSS_Analysis_GitCommitExtractor/lastSuccessfulBuild/net.ssehub.comani$comani-extractor-git/">Jenkins Download</a></td>
    <td><img src="https://jenkins-2.sse.uni-hildesheim.de/buildStatus/icon?job=OSS_Analysis_GitCommitExtractor"></td>
  </tr>
  <!-- SvnCommitExtractor -->
  <tr>
    <td><a href="https://github.com/CommitAnalysisInfrastructure/SvnCommitExtractor">SvnCommitExtractor</a></td>
    <td><b>Commit-Extractor:</b> Extract commits from subversion repositories</td>
    <td><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache License 2.0</a></td>
    <td><a href="https://jenkins-2.sse.uni-hildesheim.de/job/OSS_Analysis_SvnCommitExtractor/lastSuccessfulBuild/net.ssehub.comani.extractors$comani-extractor-svn/">Jenkins Download</a></td>
    <td><img src="https://jenkins-2.sse.uni-hildesheim.de/buildStatus/icon?job=OSS_Analysis_SvnCommitExtractor"></td>
  </tr>
  <!-- VariabilityChangeAnalyzer  -->
  <tr>
    <td><a href="https://github.com/CommitAnalysisInfrastructure/GitCommitExtractor">VariabilityChangeAnalyzer</a></td>
    <td><b>Variability-Analyzer:</b>KBuild-based Software Product Lines analyses</td>
    <td><a href="https://www.apache.org/licenses/LICENSE-2.0.html">Apache License 2.0</a></td>
    <td><a href="">Jenkins Download</a></td>
    <td><img src="https://jenkins-2.sse.uni-hildesheim.de/buildStatus/icon?job=OSS_Analysis_VariabilityChangeAnalyzer"></td>
  </tr>
</table>

## License
This project is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html).

## Acknowledgments
This work is partially supported by the ITEA3 project [REVaMP²](http://www.revamp2-project.eu/), funded by the [BMBF (German Ministry of Research and Education)](https://www.bmbf.de/) under grant 01IS16042H.

A special thanks goes to the developers of [KernelHaven](https://github.com/KernelHaven/): Adam Krafczyk, Sascha El-Sharkawy, Moritz Fl\"oter, Alice Schwarz, Kevin Stahr, Johannes Ude, Manuel Nedde, Malek Boukhari, and Marvin Forstreuter. Their architecture and core concepts significantly inspired the development of this project. In particular, the mechanisms for file-based configuration of the infrastructure and the plug-ins as well as loading and executing individual plug-ins are adopted in this work.
