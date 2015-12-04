A Distributed Evolutionary Multivariate Discretizer
=====================================================

This is an spark implementation of the Evolutionary Multivariate Discretizer algorithm, presented in [1]. This algorithm partitions the big chromosome into partitions as well as the input data. Then, several GA processes are executed over the partitions to obtain a set of selected points [1].

This software has been proved with several large real-world datasets, like:

- A dataset selected for the GECCO-2014 in Vancouver, July 13th, 2014 competition, which comes from the Protein Structure Prediction field (http://cruncher.ncl.ac.uk/bdcomp/). We have created a oversampling version of this dataset with 64 million instances, 631 attributes, 2 classes.

## Example: 
	import org.apache.spark.mllib.feature._

      	val nChr = 50
      	val ngeval = 5000
      	val mvfactor = 1
      	val alpha = .7f
      	val srate = .1f
      	val vth = 100              
              
      	println("*** Discretization method: ECPSD discretizer")
      	println("*** Number of chromosomes: " + nChr)
      	println("*** Multivariate Factor: " + mvfactor)
      	println("*** Number of genetic evaluations: " + ngeval)
	println("*** Sampling Rate: " + srate) 
      	println("*** Voting threshold: " + vth) 
              
      	val discretizer = DEMDdiscretizer.train(train,
          	contFeat,
          	nChr,
          	ngeval,
          	alpha,
          	mvfactor,
          	srate,
          	vth) 
      	discretizer
	
	val disc = data.map(i => LabeledPoint(i.label, discretizer.transform(i.features)))
	disc.first()
        

##References

[1] S. Ramírez-Gallego, S. García, J.M. Benítez, F. Herrera. Multivariate Discretization Based on Evolutionary Cut Points Selection for Classification. IEEE Transaction on Cybernetics, in press. doi: 10.1109/TCYB.2015.2410143

Soon, it will be post the correspondent contribution to the literature where this method is detailed.
