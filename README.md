# conversor-recibos

Hospedagem do **conversor público** de recibos do Receita Saúde:
**https://brunoereis.github.io/conversor-recibos/**

> Cole a planilha de atendimentos, saia com o arquivo que o Carnê-Leão do e-CAC
> importa — até 1000 recibos de uma vez, em vez de um por um no aplicativo.

## Este repositório não é o código-fonte

Aqui moram **só os dois HTML gerados**. O fonte fica em `BrunoEReis/recibos-psi`
(privado), e estes arquivos saem de lá com:

```
node scripts/conversor-standalone/montar.mjs
```

Editar `index.html` na mão é perda garantida: o próximo build sobrescreve.

## Por que os arquivos são grandes

Cada HTML carrega React, o CSS e a lógica dentro de si. **Nenhum CDN, de
propósito** — a página promete funcionar com a internet desligada, e a promessa
só vale se não houver um `<script src>` apontando para fora.

## O que ele faz com os dados

Nada. A conversão inteira acontece no navegador de quem usa. Não há servidor,
não há banco, não há analytics. Os CPFs dos pacientes não saem da máquina — é
verificável abrindo o DevTools na aba Rede e vendo que não sai requisição
nenhuma.

## Publicar de novo

```
cp ../recibos-psi/dist-conversor/*.html .
git commit -am "novo build" && git push
```

O GitHub Pages serve a branch `main`, na raiz. O `.nojekyll` existe para o Jekyll
não tentar processar nada.
