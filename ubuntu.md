# ubuntu

I run ubuntu in wsl, but these commands are generally applicable I think.

## create workspace dir

```bash
sudo mkdir /w
sudo chown bbertow. /w
```

## install standard packages with apt

```bash
sudo add-apt-repository ppa:ansible/ansible
sudo apt-get update

sudo apt install \
  corkscrew \
  ansible \
  ansible-lint \
  keychain \
  unzip \
  libxml2-utils \
  jq \
  openjdk-8-jre-headless \
  hey \
  siege \
  postgresql-client-common postgresql-client
```

## install k8s specific packages

### kubectl, kubens, kubectx

```bash
curl -LO "https://dl.k8s.io/release/v1.23.6/bin/linux/amd64/kubectl"
chmod +x ./kubectl
mv kubectl ~/.local/bin/kubectl

mkdir -p ~/.local/share/bash-completion/completions
kubectl completion bash > ~/.local/share/bash-completion/completions/kubectl
kubectl completion bash | sed 's/kubectl/k/g' > ~/.local/share/bash-completion/completions/k


curl -LO https://github.com/ahmetb/kubectx/releases/download/v0.9.4/kubectx
chmod +x ./kubectx
mv kubectx ~/.local/bin/kubectx

mkdir -p ~/.local/share/bash-completion/completions
curl -LO https://raw.githubusercontent.com/ahmetb/kubectx/master/completion/kubectx.bash
mv kubectx.bash ~/.local/share/bash-completion/completions/kubectx
cat ~/.local/share/bash-completion/completions/kubectx | sed 's/kubectx/kctx/g' > ~/.local/share/bash-completion/completions/kctx

curl -LO https://github.com/ahmetb/kubectx/releases/download/v0.9.4/kubens
chmod +x kubens
mv kubens ~/.local/bin/kubens

mkdir -p ~/.local/share/bash-completion/completions
curl -LO https://raw.githubusercontent.com/ahmetb/kubectx/master/completion/kubens.bash
mv kubens.bash ~/.local/share/bash-completion/completions/kubens
cat ~/.local/share/bash-completion/completions/kubens | sed 's/kubens/kns/g' > ~/.local/share/bash-completion/completions/kns
```

### helm

```bash

curl -LO https://get.helm.sh/helm-v3.9.2-linux-amd64.tar.gz
tar xvzf helm-v3.9.2-linux-amd64.tar.gz
tar xvzf helm-v3.9.2-linux-amd64.tar.gz --strip-components 1 linux-amd64/helm
chmod +x helm
mv helm ~/.local/bin/helm

mkdir -p ~/.local/share/bash-completion/completions
helm completion bash > ~/.local/share/bash-completion/completions/helm
```

### kind

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-linux-amd64
chmod +x ./kind
mv kind ~/.local/bin/kind

mkdir -p ~/.local/share/bash-completion/completions
kind completion bash > ~/.local/share/bash-completion/completions/kind
```