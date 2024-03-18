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

// The input data is a vector 'y' of length 'N'.
data {
  int<lower=1> N;          // number of observations
  vector[N] log_gest;// centered and standardized gestational age
  vector[N] log_bmi;
  vector[N] preterm;  // preterm indicator (0 or 1)
  vector[N] log_weight;
  vector[N] Inter;// log-transformed weight
}
parameters {
  vector[5] beta;              // coefficient for interaction term
  real<lower=0> sigma;     // error sd for Gaussian likelihood
}
model {
  // Log-likelihood
  target += normal_lpdf(log_weight | beta[1] + beta[2] * log_gest + beta[3]*preterm + beta[4]*Inter + beta[5]*log_bmi, sigma);
  // Priors
  target += normal_lpdf(sigma | 0, 1)
          + normal_lpdf(beta | 0, 1);
}
generated quantities {
  vector[N] log_lik;    // pointwise log-likelihood for LOO
  vector[N] log_weight_rep; // replications from posterior predictive dist
  
  for (n in 1:N) {
    real log_weight_hat_n = beta[1] + beta[2] * log_gest[n] + beta[3] * preterm[n] + beta[4]*Inter[n] + beta[5]*log_bmi[n];
    log_lik[n] = normal_lpdf(log_weight[n] | log_weight_hat_n, sigma);
    log_weight_rep[n] = normal_rng(log_weight_hat_n, sigma);
  }
}

