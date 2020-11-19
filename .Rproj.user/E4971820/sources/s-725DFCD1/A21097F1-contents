library(rstan)
library(sf)
library(raster)

p <- st_read("~/Downloads/Panthera_leo.shp")
clim <- stack("~/Downloads/climate.tif")
names(clim) <- c("T_max", "T_min", "P_wet", "P_dry")

stan_sdm='
data {
  int n;
  vector[n] x1;
  vector[n] x2;
  vector[n] x3;
  vector[n] x4;
  int y[n];
}
parameters {
  real a;
  real b1;
  real b2;
  real b3;
  real b4;
}
model {
  // priors
  a ~ normal(0, 10);
  b1 ~ normal(0, 10);
  b2 ~ normal(0, 10);
  b3 ~ normal(0, 10);
  b4 ~ normal(0, 10);
  // likelihood
  y ~ binomial(4, inv_logit(a + b1*x1 + b2*x2 + b3*x3 + b4*x4));
}
'

bayeSdm <- stan_model(model_code = stan_sdm)
