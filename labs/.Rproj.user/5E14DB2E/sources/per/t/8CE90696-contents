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
  y ~ normal(mu[year_i], se);
  sigma_mu ~ normal(0, 1);
  mu[1] ~ normal(0, sigma_mu);
  mu[2] ~ normal(mu[1], sigma_mu);
  for (t in 3:T) {
    mu[t] ~ normal((2*mu[t-1] - mu[t-2]), sigma_mu);
  }
}

generated quantities {
  vector[P] mu_new;
  mu_new[1] = normal_rng((2*mu[T] -  mu[T-1]), sigma_mu);
  mu_new[2] = normal_rng((2*mu_new[1] - mu[T]), sigma_mu);
  for (i in 3:P) {
    mu_new[i] = normal_rng((2*mu_new[i-1] -  mu_new[i-2]), sigma_mu);
  }
}