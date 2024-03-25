data {
  int<lower=0> N; 
  int<lower=0> T; 
  int<lower=0> mid_year; 
  vector[N] y; 
  int<lower=0> P; //Projection
  vector[N] se;
  vector[T] years; 
  int<lower=0> year_i[N]; 
  
}

parameters {
  real<lower=0> sigma_mu; 
  vector[T] mu; 
  
}

model {
  // Priors
  y ~ normal(mu[year_i], se);
  sigma_mu ~ normal(0,1);
  mu[1]~normal(0,sigma_mu);
  mu[2:T]~normal(mu[1:(T-1)],sigma_mu);
}

generated quantities {
  vector[P] mu_new;
  mu_new[1] = normal_rng(mu[T], sigma_mu);
  for (i in 2:P) {
    mu_new[i] = normal_rng(mu_new[i-1], sigma_mu);
  }
}
