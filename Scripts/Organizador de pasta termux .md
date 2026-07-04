Organização Automática de Arquivos no Android com Termux
Sistema simples para organizar automaticamente arquivos da pasta Download no Android usando scripts Bash no Termux.

Objetivo
Organizar automaticamente arquivos da pasta Download em diretórios separados por tipo:

PDFs → PDF/
Planilhas (.xlsx) → Planilhas/
Documentos (.docx) → Documentos/

## Requisitos
Termux (Android terminal environment)
Acesso ao armazenamento interno do Android
Preparação do Termux

Habilitar acesso ao armazenamento:
``
termux-setup-storage
``
Isso cria acesso ao caminho:

/storage/emulated/0/
Estrutura de pastas

O script cria automaticamente:
```
/storage/emulated/0/
 ├── Download
 ├── PDF
 ├── Planilhas
 ├── Documentos
```
Script de organização

Criar o arquivo:
```
nano organizar.sh
```
Conteúdo do script:
```
#!/data/data/com.termux/files/usr/bin/bash

BASE="/storage/emulated/0"
DOWNLOADS="$BASE/Download"

PDF="$BASE/PDF"
XLSX="$BASE/Planilhas"
DOCX="$BASE/Documentos"

mkdir -p "$PDF" "$XLSX" "$DOCX"

# PDFs
find "$DOWNLOADS" -type f -iname "*.pdf" -exec mv -f {} "$PDF/" \;

# Planilhas Excel
find "$DOWNLOADS" -type f -iname "*.xlsx" -exec mv -f {} "$XLSX/" \;

# Documentos Word
find "$DOWNLOADS" -type f -iname "*.docx" -exec mv -f {} "$DOCX/" \;

echo "Organização concluída."
```
para salvar | digite CTRL+O | Enter | CTRL+X

Permissão de execução
```
chmod +x organizar.sh
```
Execução manual
```
./organizar.sh
Automação contínua (modo simples)
```
Executa a cada 60 segundos:
```
while true; do
  ./organizar.sh
  sleep 60
done
```
