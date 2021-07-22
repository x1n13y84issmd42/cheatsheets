# SSH to an instance
```bash
heroku ps:exec -a app-name-goes-here
```

# Install `nano` to an nstance

```bash
mkdir /app/nano
curl https://github.com/Ehryk/heroku-nano/raw/master/heroku-nano-2.5.1/nano.tar.gz --location --silent | tar xz -C /app/nano
export PATH=$PATH:/app/nano
```

Works only until the dyno is alive, stops after restart/deployment.
