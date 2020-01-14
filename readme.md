# Тест "git subtree" под репозиторий для основного репозитория
Подрепозиторий может редактироваться 
1) по классическому пути
2) через другой репозиторий где тот в свою очередь будет являтся subtree  

`git subtree add -P <prefix> <commit>`  
`git subtree add -P <prefix> <repository> <ref>`  
`git subtree pull -P <prefix> <repository> <ref>`  
`git subtree push -P <prefix> <repository> <ref>`  
`git subtree merge -P <prefix> <commit>`  
`git subtree split -P <prefix> [OPTIONS] [<commit>]`  

## Пример

### Подготовка коренгого репозитория  
- `git init`  
- `комитим что-нибудь`  

### Добавление субрепо в руутрепо
- `git remote add subtree-remote https://github.com/Alexey808/git-subtree-test.git`  
- `git subtree add --prefix=git-subtree-test/ subtree-remote master`  

### Если нужно изменить субрепо из руутрепо  
- `комитим что-нибудь`  
- `git subtree push -P git-subtree-test/ subtree-remote master`  

### Подтянуть последние изменения  
- `git fetch subtree-remote master`  
- `git subtree pull -P git-subtree-test/ subtree-remote master`  

# Доступ к дочернему скрипту в package.json  
`npm run test` = root repo  
`npm run subtree test` = subtree repo  

Имея такую структуру скриптов

**руутрепо, package.json**
```
  "scripts": {
    "test": "echo 'root repo'",
    "subtree": "cd git-subtree-test && npm run"
  }
```

**подрепо, package.json**
```
  "scripts": {
    "test": "echo 'subtree repo'",
  }
```

