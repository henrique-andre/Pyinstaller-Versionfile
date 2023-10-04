# pyinstaller-versionfile

Versionamento simples para projetos  Python transformados em executáveis(.exe) do Windows a partir de um arquivo .TXT  que pode ser usado pelo PyInstaller.

## Informações
pyinstaller-versionfile fornece alguns parâmetros para adicionar ao executável em sua criação, segue exemplos abaixo.



|  Parâmetros  | Descrição                                                                                                                                                                                                                                 |
|:----------------:|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   CompanyName    | Nome da empresa que produziu o arquivo, por exemplo, "My Imaginary Company, Inc.".                                                                                                                 |
| FileDescription  | Descrição a ser apresentada aos usuários. Pode ser exibido quando o usuário está escolhendo os arquivos a serem instalados. Por exemplo, "Um aplicativo simples que faz coisas simples"                                                                                |
|   InternalName   | Nome interno do arquivo. Se o arquivo não tiver nome interno, esta string deverá ser o nome do arquivo original, sem extensão. Por exemplo, 'Aplicativo Simples'.                                                                                     |
|  LegalCopyright  | Avisos de direitos autorais que se aplicam ao arquivo. Isto deve incluir o texto completo de todos os avisos, símbolos legais, datas de direitos autorais e assim por diante. Por exemplo, "Copyright © 2000-2022, My Imaginary Company, Inc. Todos os direitos reservados".               |
| OriginalFilename | Nome original do arquivo, sem incluir o caminho. Essas informações permitem que um aplicativo determine se um arquivo foi renomeado por um usuário. Por exemplo, "SimpleApp.exe".
                                                              

## Como usar
pyinstaller-versionfile fornece uma interface funcional para criar , siga esses passos:

1º Em seu editor de código Visual Studio ou PyCharm crie um arquivo python com o nome `"versionfile.py"` ou o nome que desejar

2° Abra o terminal no editor de código e importe a biblioteca em sua máquina ou ambiente virtual:

` pip install pyinstaller-versionfile `


### Interface da Linha de comando
Com o arquivo .py criado, copie esse código abaixo e ajuste as informações de versão conforme o desejado para seu arquivo .exe para passar para o PyInstaller através da opção `--version-file=` e execute o comando.


``` Python
import pyinstaller_versionfile

pyinstaller_versionfile.create_versionfile(
    output_file="versionfile.txt",
    version="1.2.3.4",
    company_name="My Imaginary Company",
    file_description="Simple App",
    internal_name="Simple App",
    legal_copyright="© My Imaginary Company. All rights reserved.",
    original_filename="SimpleApp.exe",
    product_name="Simple App",
    translations=[0, 1200]
)
```

Ao executar irá ser criado um arquivo `versionfile.txt` na raiz do projeto que ira conter as seguintes informações:

``` CSS
# UTF-8
#
# For more details about fixed file info 'ffi' see:
# http://msdn.microsoft.com/en-us/library/ms646997.aspx

VSVersionInfo(
  ffi=FixedFileInfo(
    # filevers and prodvers should be always a tuple with four items: (1, 2, 3, 4)
    # Set not needed items to zero 0. Must always contain 4 elements.
    filevers=(1,2,3,4),
    prodvers=(1,2,3,4),
    # Contains a bitmask that specifies the valid bits 'flags'r
    mask=0x3f,
    # Contains a bitmask that specifies the Boolean attributes of the file.
    flags=0x0,
    # The operating system for which this file was designed.
    # 0x4 - NT and there is no need to change it.
    OS=0x40004,
    # The general type of file.
    # 0x1 - the file is an application.
    fileType=0x1,
    # The function of the file.
    # 0x0 - the function is not defined for this fileType
    subtype=0x0,
    # Creation date and time stamp.
    date=(0, 0)
    ),
  kids=[
    StringFileInfo(
      [
      StringTable(
        u'040904B0',
        [StringStruct(u'CompanyName', u'My Imaginary Company'),
        StringStruct(u'FileDescription', u'Simple App'),
        StringStruct(u'FileVersion', u'1.2.3.4'),
        StringStruct(u'InternalName', u'Simple App'),
        StringStruct(u'LegalCopyright', u'© My Imaginary Company. All rights reserved.'),
        StringStruct(u'OriginalFilename', u'SimpleApp.exe'),
        StringStruct(u'ProductName', u'Simple App'),
        StringStruct(u'ProductVersion', u'1.2.3.4')])
      ]), 
    VarFileInfo([VarStruct(u'Translation', [0, 1200])])
  ]
)
```



## Finalizando

Ao formar o comando para criar o executavel forneça o seguinte parametro `--version-file=versionfile.txt` ex:

pyinstaller --onefile --icon="caminho do icone se houver" --noconsole `--version-file=versionfile.txt` projeto.py"

Confira em propriedades - detalhes do .exe as informações construidas.


