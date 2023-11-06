---
layout: internal
---

dotnet
Listar os sdks presentes na máquina
dotnet --list-sdks
Listar os templates disponíveis
dotnet new --list
Criação do arquivo globaljson
dotnet new globaljson --sdk-version 5.0.404 --output HealthCheckSln/HealthCheck
Criando um projeto Angular e WebApi
dotnet new angular -o HealthCheckSln/HealthCheck --framework net5.0
dotnet new webapi -o CompanyEmployeesSln/CompanyEmployees --framework net5.0
Criação da solução
dotnet new sln -o HealthCheckSln
Adicionar o projeto a solução
dotnet sln HealthCheckSln add HealthCheckSln/HealthCheck
Adicionando projeto de teste
dotnet new xunit -o SportsSln/SportsStore.Tests --framework net5.0
dotnet sln SportsSln add SportsSln/SportsStore.Tests
dotnet add SportsSln/SportsStore.Tests reference SportsSln/SportsStore
Adicionando package ao projeto
dotnet add SportsSln/SportsStore.Tests package Moq --version 4.13.1
Removendo pacote do projeto
dotnet remove SportsSln/SportsStore.Tests package Moq
Para executar a aplicação
dotnet run
Para usar o SQL Server no projeto
dotnet add package Microsoft.EntityFrameworkCore --version 5.0.0
dotnet add package Microsoft.EntityFrameworkCore.Tools --version 5.0.0
dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 5.0.0
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL --version 5.0.0
Para instalar o pacote de ferramentas do Entity Framework globalmente
dotnet tool uninstall --global dotnet-ef
dotnet tool install --global dotnet-ef --version 5.0.0
Para listar os pacotes instalados globalmente
dotnet tool list --global
Para adicionar migrações
dotnet ef migrations add “Initial”
dotnet ef migrations add “Initial” -o "Data/Migrations"
Para remover migrações
dotnet ef migrations remove
Para aplicar a migration
dotnet ef database update
Para resetar o banco de dados
dotnet ef database drop --force --context StoreDbContext
NVM - Node version manager (<https://docs.microsoft.com/pt-br/windows/dev-environment/javascript/nodejs-on-wsl>)
Para saber se o nvm está instalado
command -v nvm   (tem que responder com ‘nvm’)
Para listar a versões do node instaladas
nvm ls
Para instalar a versão LTS estável do node
nvm install --lts
Para alternar entre versões o procedimento é o seguinte
Para alterar a versão do Node.js que você deseja usar para um projeto, crie um diretório de projeto mkdir NodeTest e insira o diretório cd NodeTest. Em seguida, digite nvm use node para alternar para a versão atual ou nvm use --lts para alternar para a versão LTS. Você também pode usar o número específico para qualquer versão adicional instalada, como nvm use v8.2.1.
NPM
Listar as packages instaladas globalmente
npm list -g --depht=0
Para instalar uma package globalmente
npm install -g npm-check-updates  (ncu -g)
npm install -g npm-windows-upgrade
npm install -g npkill
Desinstalar uma package instalada globalmente
npm uninstall -g package-name
Para instalar uma package de desenvolvimento
npm install package-name --save-dev
para criar um novo projeto sem ter o “ng cli” instalado globalmente
na pasta dev, npx @angular/cli new nome-proj-app   (@angular/cli == ng)
dentro da pasta do nome-proj-app vc já pode usar o “npx ng” normalmente, porque o pacote do angular está instalado na pasta node_modules
para iniciar a aplicação angular
npm start
para rodar o teste
npm test
para compilar a aplicação angular
npm run build
Procedimento a ser feito quando baixa um projeto do git, onde não existe a pasta node_modules
npm install
npm update
Angular CLI
Para criar um novo componente
npx ng generate component nav-menu --skipTests=true
npx ng generate component home --skipTests=true
Para instalar o Angular Material
npx ng add @angular/material
Angular structural directive
*ngIf
<p *ngIf="!cities"><em>Loading...</em></p>
*ngFor
<tr *ngFor="let city of cities">
Angular Bind
property binding (component → HTML element)
<table class='table table-striped' aria-labelledby="tableLabel" [hidden]="!cities">
Angular form
Template-Driven Forms
O formulário é construído no arquivo .html do componente
Cada campo de input está associado a uma instância ngModel através de Binding de dados
Usa um objeto ngForm relacionado a todo o formulário
<form novalidate autocomplete="off" #form="ngForm" (ngSubmit)="onSubmit(form)">
 <input type="text" name="name" value="" required placeholder="Insert the city name..."
 [(ngModel)]="city.Name" #title="ngModel"/>
 <span*ngIf="(name.touched || name.dirty) && name.errors?.required">
  Name is a required field: please enter a valid city name.
 </span>
 <button type="submit" name="btnSubmit" [disabled]="form.invalid">Submit</button>
</form>
Model-Driven Form (também conhecido como Reactive Forms)
O template html apenas referencia um objeto TypeScript mais complexo (o form model) que é definido, instanciado e configurado programaticamente dentro do classe .ts.
<form [formGroup]="form" (ngSubmit)="onSubmit()">
   <input formControlName="name" required />
     <span *ngIf="(form.get('name').touched || form.get('name').dirty) && form.get('name').errors?.required">
        Name is a required field: please enter a valid city name.
     </span>
 <button type="submit" name="btnSubmit" [disabled]="form.invalid">Submit</button>
</form>
