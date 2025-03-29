# Argos Translate
[Demo](https://libretranslate.com) | [Website](https://www.argosopentech.com) | [Docs](https://argos-translate.readthedocs.io) |  [Forum](https://community.libretranslate.com/c/argos-translate/5) | [GitHub](https://github.com/argosopentech/argos-translate) | [PyPI](https://pypi.org/project/argostranslate/)

**Biblioteca de tradução de código aberto escrita em Python**

Argos Translate utiliza [OpenNMT](https://opennmt.net/) para as traduções e pode ser utilizado como biblioteca do Python, linha de comandos ou aplicação GUI. Argos Translate suporta a instalação de pacotes modelo de idiomas que são arquivos zip com a extensão ".argosmodel" que contém os dados necessários para a tradução. [LibreTranslate](https://libretranslate.com) é uma API e aplicação da Web criada no topo do Argos Translate.

Argos Trañslate também gere automaticamente que gira pelos idiomas intermediários para traduzir entre os idiomas que não têm uma tradução direta entre eles instalados. Por exemplo, se tiver uma tradução de ES → EN e EN → FR instalada, poderá traduzir de ES → FR como se tivesse a tradução instalada. Isto permite traduzir entre uma ampla variedade de idiomas ao custo de alguma perda de qualidade da tradução.

O [argospm-index](https://github.com/argosopentech/argospm-index) contains metadata and download links to access pre-trained Argos Translate models.

### Idiomas suportados
Alemão, Árabe, Arzebajão, Catalão, Chinês, Checo, Dinamarquês, Eslovaco, Espanhol, Esperanto, Holandês, Inglês, Finnish, Francês, Grego, Hebrew, Indiano (Hindi), Húngaro, Indonesian, Irish, Italiano, Japonês, Coreano, Malay, Persa, Polaco, Português (Brazil), Português (Portugal), Russo, Sueco, Turco, Ucraniano, e muito mais.

[Solicitar um idioma](https://github.com/argosopentech/argos-translate/discussions/91)

## Instalação
### Instalar com Python
Argos Translate is available from [PyPI](https://pypi.org/project/argostranslate/) and can be easily installed or updated with [pip](https://pip.pypa.io/en/stable/installation/).

```
pip install argostranslate
```

Install [GUI](https://github.com/argosopentech/argos-translate-gui):
```
pip install argostranslategui
```

### Python source installation into virtualenv

Download a copy of this repo and install with pip.

```
git clone https://github.com/argosopentech/argos-translate.git
cd argos-translate
virtualenv env
source env/bin/activate
pip install -e .
```

## Exemplos
### [Python](https://argos-translate.readthedocs.io/en/latest/py-modindex.html)

```python
import argostranslate.package
import argostranslate.translate

from_code = "en"
to_code = "es"

# Download and install Argos Translate package
argostranslate.package.update_package_index()
available_packages = argostranslate.package.get_available_packages()
package_to_install = next(
    filter(
        lambda x: x.from_code == from_code and x.to_code == to_code, available_packages
    )
)
argostranslate.package.install_from_path(package_to_install.download())

# Translate
translatedText = argostranslate.translate.translate("Hello World", from_code, to_code)
print(translatedText)
# '¡Hola Mundo!'
```

### Interface da Linha de Comandos
```
argospm update
argospm install translate-en_de
argos-translate --from en --to de "Hello World!"
# Hallo Welt!

```

Install all translation packages:
```
argospm install translate
```

### [LibreTranslate](https://github.com/LibreTranslate/LibreTranslate) Web App ([Demo](https://libretranslate.com/))
![Web App Screenshot](img/WebAppScreenshot.png)

### [LibreTranslate](https://github.com/uav4geo/LibreTranslate) API

```javascript
const res = await fetch("https://translate.argosopentech.com/translate", {
	method: "POST",
	body: JSON.stringify({
		q: "Hello!",
		source: "en",
		target: "es"
	}),
	headers: {
		"Content-Type": "application/json"}
	});

console.log(await res.json());

{
    "translatedText": "¡Hola!"
}
```

#### Graphical user interface
The GUI code is in a [separate repository](https://github.com/argosopentech/argos-translate-gui).

![Screenshot](/img/Screenshot.png)
![Screenshot2](/img/Screenshot2.png)


## [Packages](https://www.argosopentech.com/argospm/index/)
- [Browse](https://www.argosopentech.com/argospm/index/)
- [P2P download with BitTorrent](/p2p/README.md)
- [Training scripts](https://github.com/argosopentech/argos-train)
- [Google Drive download](https://drive.google.com/drive/folders/11wxM3Ze7NCgOk_tdtRjwet10DmtvFu3i)


### Aceleração de GPU

To enable GPU support, you need to set the `ARGOS_DEVICE_TYPE` env variable to `cuda` or `auto`.

```
$ ARGOS_DEVICE_TYPE=cuda argos-translate --from-lang en --to-lang es "Hello World"
Hola Mundo
```

The above env variable passes the device type to [CTranslate2](https://github.com/OpenNMT/CTranslate2).

### Tradução de HTML
The [translate-html](https://github.com/argosopentech/translate-html) library is built on top of Argos Translate and [Beautiful Soup](https://beautiful-soup-4.readthedocs.io/en/latest/) and parses and translates HTML. The LibreTranslate API also has support for translating HTML.


### Tradução de Ficheiros
The [argos-translate-files](https://github.com/LibreTranslate/argos-translate-files) library is built on top of Argos Translate and parses and translates files. The LibreTranslate API also has support for translating files.

## Desintalação

``` shell
pip uninstall argostranslate
```

You may choose to also delete temporary and cached files:

``` shell
rm -r ~/.local/cache/argos-translate
rm -r ~/.local/share/argos-translate
```

## Projetos Relacionados
- [LibreTranslate-py](https://github.com/argosopentech/LibreTranslate-py) - Python bindings for LibreTranslate
- [MetalTranslate](https://github.com/argosopentech/MetalTranslate) - Customizable translation in C++
- [LibreTranslate/Locomotive](https://github.com/LibreTranslate/Locomotive) - Toolkit for training/converting LibreTranslate compatible language models 🚂 
- [DesktopTranslator](https://github.com/ymoslem/DesktopTranslator) - [OpenNMT](https://opennmt.net/) based translation application
- [LibreTranslate-rs](https://github.com/grantshandy/libretranslate-rs) - LibreTranslate Rust bindings
- [LibreTranslate Go](https://github.com/SnakeSel/libretranslate) - LibreTranslate Golang bindings
- [LibreTranslate Java](https://github.com/dynomake/libretranslate-java) - LibreTranslate Java bindings
- [LibreTranslator](https://gitlab.com/BeowuIf/libretranslator) - LibreTranslate Android app
- [LiTranslate](https://community.libretranslate.com/t/litranslate-ios-app/333) - iOS LibreTranslate client

## Colaboração
As colaborações são bem-vindas! Available issues are on the [GitHub issues page](https://github.com/argosopentech/argos-translate/issues). Contributions of code, data, and pre-trained models can all be accepted.

## Apoio
For support please use the [LibreTranslate Forum](https://community.libretranslate.com/c/argos-translate/5) or [GitHub Issues](https://github.com/argosopentech/argos-translate/issues).

For questions about [CTranslate2](https://github.com/OpenNMT/CTranslate2) or general machine translation research the [OpenNMT Forum](https://forum.opennmt.net/) is a good resource.

## Serviços
Custom models trained on your own data are available for $1000/language (negotiable).

[I am also available for hire](https://www.argosopentech.com/about/) to do support, consulting, or custom software development.

## Doar
If you find this software useful donations are greatly appreciated and help to make this project sustainable.
- [GitHub Sponsor](https://github.com/sponsors/argosopentech)
- [PayPal](https://www.paypal.com/biz/fund?id=MCCFG437JP9PJ)
- Bitcoin: 16UJrmSEGojFPaqjTGpuSMNhNRSsnspFJT
- Ethereum: argosopentech.eth
- Litecoin: MCwu7RRWeCRJdsv2bXGj2nnL1xYxDBvwW5
- BCH: bitcoincash:qzvpxe8y5kq45kahqkyv3p88sjrhlymj2v6xdrj3cv

Paid supporters receive priority support.

#### Hosting affiliate links
You can help support Argos Translate financially by purchasing hosting through these referral links:
- [Vast.ai](http://vast.ai/?ref=24817) - Cheap GPU rentals
- [DigitalOcean](https://m.do.co/c/a1af57be6e3f) - Best all around hosting
- [Sharktech](https://portal.sharktech.net/aff.php?aff=1181) - Cheap bandwith
- [Time4VPS](https://www.time4vps.com/?affid=6929) - Cheap storage

## Contribuição
Contributions are welcome! Bug reports, pull requests, documentation writing, and feature ideas are all appreciated.

## Licença
Argos Translate is dual licensed under either the [MIT License](https://github.com/argosopentech/argos-translate/blob/master/LICENSE) or [Creative Commons CC0](https://creativecommons.org/share-your-work/public-domain/cc0/).
