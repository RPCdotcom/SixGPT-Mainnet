# SixGPT Setup Rehber

![image](https://github.com/user-attachments/assets/155f4f07-c894-4197-afd5-ba1028531fa0)

Bu rehber, bir WEb miner'ını Ubuntu sunucusunda yapılandırmak için gerekli kurulum adımlarını içerir. İçerisinde; Docker ve Docker Compose kurulumu, izinlerin ayarlanması, sixgpt dosyası oluşturulması ve Container'in çalıştırılması gibi adımlar yer almaktadır.

## Server  : 
- Contabo : https://bit.ly/contabourl 
- PQ : https://pq.hosting/?from=627713 
- Hetzner : https://hetzner.cloud/?ref=ASjlHtRt2swV 
- Digital Ocean : https://digitalocean.pxf.io/q465nn

## Gereksinimler
- Ubuntu sunucusu
- Ssh bağlantı aracı

## Sunucu Özellikleri 

- Min : 4 CPU 6+ RAM 50 GB SSD

## 1. Sistemi Güncelle ve Yükselt

Sistem paketlerini güncellemek ve yükseltmek için aşağıdaki komutu çalıştırın:

```bash
sudo apt update -y && sudo apt upgrade -y
```
## 2. Gerekli paketleri kurun:

```bash
sudo apt install htop ca-certificates zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev tmux iptables curl nvme-cli git wget make jq libleveldb-dev build-essential pkg-config ncdu tar clang bsdmainutils lsb-release libssl-dev libreadline-dev libffi-dev jq gcc screen unzip lz4 -y
```
## 3. Docker'ı Kur : 

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
docker version
```

## 4. Docker Compose'u Kur : 

```bash
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -L "https://github.com/docker/compose/releases/download/$VER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## 4. Docker Kullanıcı İzinleri

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

## 5. sixgpt Dizinini İndirme :

```bash
git clone https://github.com/sixgpt/miner.git
```

```bash
cd miner
```

## 6. .env Dosyasını Oluşturma ve Düzenleme : 

```bash
nano .env
```

### Buradaki PrivateKey Kısmına Metamask Cüzdan private keyinizle değiştirin. Sonrasında topluca yapıştırın.

```bash
VANA_PRIVATE_KEY=burayaprivkeyyaz
VANA_NETWORK=mainnet
OLLAMA_API_URL=http://ollama:11434/api
```

## 7. Minerı Başlat : 

```bash
docker-compose up -d
```

8. Loglar : 

```bash
docker-compose logs -f
```

