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

## install docker-compose

```bash
curl -L "https://github.com/docker/compose/releases/download/v2.9.0/docker-compose-linux-x86_64" -o ~/.local/bin/docker-compose
chmod +x ~/.local/bin/docker-compose

mkdir -p ~/.local/share/bash-completion/completions
curl \
    -L https://raw.githubusercontent.com/docker/compose/2.9.0/contrib/completion/bash/docker-compose \
    -o ~/.local/share/bash-completion/completions/docker-compose
```

## install sqlite

```bash
wget -c https://www.sqlite.org/2022/sqlite-amalgamation-3390200.zip
unzip sqlite-amalgamation-3390200.zip
cd sqlite-amalgamation-3390200/
gcc shell.c sqlite3.c -lpthread -ldl -lm -o sqlite3
mv sqlite3 ~/.local/bin/
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

### k9s

```bash
cd /w
git clone git@github.com:derailed/k9s.git
make build
mv execs/k9s ~/.local/bin/k9s

mkdir -p ~/.local/share/bash-completion/completions
k9s completion bash > ~/.local/share/bash-completion/completions/k9s
```

### linkerd

```bash
curl -L https://github.com/linkerd/linkerd2/releases/download/stable-2.12.2/linkerd2-cli-stable-2.12.2-linux-amd64 -o linkerd
chmod +x ./linkerd
mv linkerd ~/.local/bin/linkerd

mkdir -p ~/.local/share/bash-completion/completions
linkerd completion bash > ~/.local/share/bash-completion/completions/linkerd
```

