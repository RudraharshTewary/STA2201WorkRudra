
data {
  int<lower=0> N; 
  int<lower=0> T; 
  int<lower=0> mid_year; 
  vector[N] y; 
  vector[N] se;
  int<lower=0> P; // Projection
  vector[T] years; 
  int<lower=0> year_i[N]; 
  
}

parameters {
  real alpha;
  real beta;

}

transformed parameters{
  vector[T] mu;
  
  for(t in 1:T){
    mu[t] = alpha + beta*(years[t] - mid_year);
  }
}

model {
  
  y ~ normal(mu[year_i], se);
  
  alpha ~ normal(0, 1);
  beta ~ normal(0,1);
}

generated quantities{
  vector[P] mu_new;
  for (i in 1:P){
  mu_new[i] = alpha + beta * (years[T]+i- mid_year);
  }
}