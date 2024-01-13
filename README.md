# ICU_bed_Simulation

This simulation was originally written as part of ESICM 5th critical care [datathon](https://www.esicm.org/events/datathon-2023/programme/) and is based on the data provided by AmsterdamUMCdb. You can get access to this database by following the instructions at https://github.com/AmsterdamUMC/AmsterdamUMCdb. 
There is an extensive explanation about the database at https://github.com/AmsterdamUMC/AmsterdamUMCdb/wiki which helps to get familiarize with the information stored in the AmsterdamUMCdb database.
In this simulation, we only use admissions data (https://github.com/AmsterdamUMC/AmsterdamUMCdb/wiki/admissions). 

The simulation was primarily designed to predict a situation where the distribution of admitted patients matched the real data provided by AmsterdamUMCdb. However, the option to create a distribution to simulate a pandemic-like event was included in the code. In the pandemic-like simulation, the distribution of admissions is given by those patients in the database whose respiratory Sofa score represents an ARDS condition. Switching between these two events is controlled via a variable called `pandemic` with a `boolean` value. 

The calculation of the distribution of ICU bed admission rates is done using three different approaches: 

- Using a Log-Normal Distribution with the mean ($\mu$) of the logarithm of the distribution obtained from the real data, $\mu=\log(\textrm{average admissions})$, and the standard deviation ($\sigma$) sets to fit the AmsterdamUMCdb profile for admitted patients
  $$P(x) = \frac{1}{\sigma x \sqrt{2\pi} } e^{-\frac{(\ln{x}-\mu)^2}{2\sigma^2}}$$ 
- Using a Poisson Distribution with the expected value ($\lambda$) of distribution set to be the mean length of stay obtained from the real data, based on AmsterdamUMCdb mean=22 (See the description of data in the [real data simulation]((/arash_ranjbar/ICU_bed_Simulation/Simulation_ARDS_(Pandemic).ipynb)) or[pandemic simulation](/arash_ranjbar/ICU_bed_Simulation/Simulation_ARDS_(Pandemic).ipynb))
  $$f(k;\lambda)= P(x=k) = \frac{\lambda^k e^{-\lambda}}{k!}, \qquad\qquad k=\textrm{admission rate}$$ 
- Random choice of length of stays weighted using the probability of Planned, Emergency, or Pandemic ARDS distribution calculated in the files.

Continues ... 
