//
// This Stan program defines a simple model, with a
// vector of values 'y' modeled as normally distributed
// with mean 'mu' and standard deviation 'sigma'.
//
// Learn more about model development with Stan at:
//
//    http://mc-stan.org/users/interfaces/rstan.html
//    https://github.com/stan-dev/rstan/wiki/RStan-Getting-Started
//

data {
  int<lower=0> N; // Number of regions
  vector[N] aff_i; // Proportion of male population working outside in each region
  int<lower=0> observe[N]; // Observed deaths in each region
  vector[N] expect_i; // Expected deaths in each region
}

parameters {
  real alpha; // Intercept
  real<lower=0> beta; // Coefficient for proportion of male population
}

transformed parameters{
  vector[N] theta;
  for (i in 1:N){
    theta[i] = alpha + beta*aff_i[i];
  }
}

model {
  alpha ~ normal(0,1);
  beta ~ normal(0,1);
  observe ~ poisson(expect_i .* exp(theta));
}
generated quantities{
  vector[N] log_lik;
  for (i in 1:N){
  real observe_hat = expect_i[i] * exp(theta[i]);
  log_lik[i] = poisson_lpmf(observe[i] | observe_hat);
  }
}

