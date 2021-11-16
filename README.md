# es-vietnamese-docker
This is a mi
**Disclaimer** 
- This repo is for single node ES, you can update the docker build as your requirements.
- I don't know how Java, or C++ package build works, some steps may be can do inside Docker.

# Steps to add Vietnamese es plugin

## TL;DR: 
Checkout my instruction on [Youtube](https://www.youtube.com/watch?v=aAuW_wV81Xk)

1. Clone the cococ library repository 

```sh
git clone https://github.com/coccoc/coccoc-tokenizer.git
cd coccoc-tokenizer && mkdir build && cd build
cmake -DBUILD_JAVA=1 ..
make install
```

2. Copy the `/usr/local/share/tokenizer/dicts` folder to this repo `/elasticsearch/dicts` directory

3. Clone the plugin
```sh
git clone https://github.com/duydo/elasticsearch-analysis-vietnamese.git
```
Update `elasticsearch-analysis-vietnamese/pom.xml` file to expected version (I'm using `7.14.2`)

```xml
<groupId>org.elasticsearch</groupId>
<artifactId>elasticsearch-analysis-vietnamese</artifactId>
<version>7.4.0</version>
```

then run `mvn package` to build the plugin

4. Copy the `elasticsearch-analysis-vietnamese/release/elasticsearch-analysis-vietnamese-7.14.2.zip` folder to this repo `/elasticsearch/` directory

5. Update the version in `.env` file to match with the version of plugin

6. Run docker compose - Bingo!

Thank you, good luck!

