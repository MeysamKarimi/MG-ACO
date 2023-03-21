# Ant-Colony Optimization (ACO) for model generation
This repository contains the prototype tool supporting the work in [1] that applies ACO for model generation with the aim of model transformation testing. It also contains the results of the experiments, with the corresponding files. 


## Prototype tool 
It has been developed with Eclipse Modeling Tools, version IDE 2020-06 (4.16.0). The following plugins are needed: MDE Testing Framework [2], anATLyzer [3] and ATL.

Folder "src" contains the source code written in Java 11. Folder "resources" contains inputs related to the case studies, including metamodels, OCL constraints and VQL constraints. As an example "Families.ecore", which is used as running example in [1], is located in this folder. Folder "Moldes" will hold the generated models after running the tool.

To run the program with desired settings, three parts can be changed in "App.java" file:
* The "loadMetamodel" method where the user can define the desired metamodel.
* The "loadOclRules" method where the user can define an ocl file containing ocl constraints.
* Arbitrary parameters such as "elementCount", "modelCount", as well as ACO algorithm parameters including "rounds", "populationCount", "alpha" and "beta", which can be defined in the "DiscoveredPath" and "ACO" constructors.

Please note that the population of ants must be equal or greater than the number of requested models. Once, all desired settings are applied, you could easily run the app and see the models as the output.

## Mutation Analysis

Part of the evaluation of this tool consists in mutation analysis. 

This project contains the mutation analysis performed on five case studies explained in [1]. Folder “analysis” contains all the artifacts regarding each of the case studies. For instance, there are three folders, containing zip files, named ACO, Viatra and Random that contain the mutation analysis for the three tools [1]. "ACO" refers to our approach, while "Viatra" and "Random" refer to the approaches with which we compare our approach in [1].

In each of the zip files, there is one folder for each of the case studies. Within each of these folders, there are thirty folders with the mutation results for the 30 different runs. In each Run, there is a folder named "models-X" that contains the model generated by the corresponding approach and other three folders, namely "zoo", "mottu" and "wimmer" that refer to typing, semantic and syntax mutants, respectively [1][2]. Mutants, mutant-killing models and sample of output models resulting from the running of the mutants can be found in each related folder. 

In order to re-execute results with the different case studies and the different mutants, some lines of code in [2] must be commented and uncommented. After doing so, the class can be executed by right-clicking and selecting Run As -> JUnit Plug-in Test. The code in this Java class contains explanations for executing each case study, for instance:

```java
String testcase = "Grafcet2PetriNet";
String[] metamodelFiles = new String[] { metamodel(testcase, "Grafcet.ecore"), metamodel(testcase, "PetriNet.ecore") };
String[] metamodelNames = new String[] { "Grafcet", "PetriNet" };	
AtlTransformation trafo = AtlTransformation.fromFile(trafo("Grafcet2PetriNet", "Grafcet2PetriNet.atl"), metamodelFiles, metamodelNames);
```

After executing the program, some information will be displayed in the console. This information can be seen in a txt file named "Report" that is located in each run folder indicates the result of each of the mutation analysis.

## Performance

Regarding the measurement of the performance of different approaches, as described in the paper [1], thirty different executions were performed with different numbers and sizes of models in each approach. These results can be seen in the Performance.xlsx file. 

## References

[1] Meysam Karimi, Shekoufeh Kolahdouz-Rahimi, Javier Troya. "Test model generation for model transformation testing applying ant colony optimization". Submitted, 2023

[2] Guerra, E., Cuadrado, J. S., & de Lara, J. (2019). Towards Effective Mutation Testing for ATL. In 22nd ACM/IEEE International Conference on Model Driven Engineering Languages and Systems, MODELS 2019, Munich, Germany, September 15-20, 2019 (pp. 78–88). IEEE. doi: 10.1109/MODELS.2019.00-13.

[3] J. S´anchez Cuadrado, E. Guerra, and J. de Lara, “Static analysis of model transformations,” IEEE Trans. Software Eng., vol. 43, no. 9, pp. 868–897, 2017.
