# Git-ის პრაქტიკული დავალება — სამივე ეტაპი

## დაწყებამდე
1. დააყენე Git და შედი GitHub-ის ანგარიშში ბრაუზერიდან.
2. გახსენი ტერმინალი ამ საქაღალდეში (`exam-project`).
3. ქვემოთ მოცემული ბრძანებები შეასრულე თანმიმდევრობით.
4. GitHub-ზე შექმენი **Public** რეპოზიტორი სახელით `exam-project`. შექმნისას არ დაამატო README, .gitignore ან license.

> თუ `git config` ჯერ არ გაქვს დაყენებული, ერთხელ შეასრულე:
```bash
git config --global user.name "შენი სახელი"
git config --global user.email "შენი GitHub-ის ელფოსტა"
```

## I ეტაპი — ლოკალური რეპოზიტორი და GitHub

თუ ამ საქაღალდეში ჯერ არ გაქვს Git რეპოზიტორი, შეასრულე:

```bash
git init
git branch -M main
git add .
git commit -m "Create initial project files"
git remote add origin https://github.com/შენი-USERNAME/exam-project.git
git push -u origin main
```

`შენი-USERNAME` შეცვალე შენი GitHub მომხმარებლის სახელით.

თუ ტერმინალი წერს, რომ `origin` უკვე არსებობს, გამოიყენე:
```bash
git remote set-url origin https://github.com/შენი-USERNAME/exam-project.git
```

## II ეტაპი — branch-ის შექმნა და merge

შექმენი ახალი branch და გადადი მასზე:

```bash
git checkout -b feature-header
```

`index.html`-ში, `<body>`-ის დასაწყისში, დაამატე ეს header:

```html
<header>
    <h1>Exam Project</h1>
    <p>Git-ის პრაქტიკული დავალება</p>
</header>
```

შეინახე ფაილი და შეასრულე:

```bash
git add index.html
git commit -m "Add project header"
git push -u origin feature-header
git checkout main
git merge feature-header
git push origin main
```

## III ეტაპი — merge conflict-ის შექმნა და მოგვარება

### 1. პირველი branch
```bash
git checkout main
git checkout -b nav-feature
```

`index.html`-ში, header-ის ქვემოთ დაამატე ნავიგაცია:

```html
<nav>
    <a href="#home">მთავარი</a>
    <a href="#about">ჩვენ შესახებ</a>
</nav>
```

შეინახე და დააკომიტე:
```bash
git add index.html
git commit -m "Add primary navigation"
git push -u origin nav-feature
```

### 2. მეორე branch — იგივე ადგილის განსხვავებული ცვლილება
```bash
git checkout main
git checkout -b nav-alt
```

`index.html`-ში ზუსტად იმავე ადგილას დაამატე სხვა ნავიგაცია:

```html
<nav>
    <a href="#courses">კურსები</a>
    <a href="#contact">კონტაქტი</a>
</nav>
```

შეინახე და დააკომიტე:
```bash
git add index.html
git commit -m "Add alternative navigation"
git push -u origin nav-alt
```

### 3. Merge და კონფლიქტის დაფიქსირება
```bash
git checkout main
git merge nav-feature
git merge nav-alt
```

მეორე merge-ზე მოსალოდნელია კონფლიქტი, რადგან ორივე branch-ში ერთსა და იმავე ადგილას განსხვავებული კოდი დაემატა.

გახსენი `index.html`. Git-ის მარკერები დაახლოებით ასე გამოჩნდება:

```text
<<<<<<< HEAD
<nav>
    <a href="#home">მთავარი</a>
    <a href="#about">ჩვენ შესახებ</a>
</nav>
=======
<nav>
    <a href="#courses">კურსები</a>
    <a href="#contact">კონტაქტი</a>
</nav>
>>>>>>> nav-alt
```

### 4. კონფლიქტის მოგვარება
მარკერები (`<<<<<<<`, `=======`, `>>>>>>>`) წაშალე და ორივე ნავიგაცია გააერთიანე. მაგალითად, საბოლოო კოდი იყოს:

```html
<nav>
    <a href="#home">მთავარი</a>
    <a href="#about">ჩვენ შესახებ</a>
    <a href="#courses">კურსები</a>
    <a href="#contact">კონტაქტი</a>
</nav>
```

შეინახე `index.html` და დაასრულე merge:

```bash
git add index.html
git commit -m "Resolve merge conflict by combining navigation links"
git push origin main
```

## შემოწმება

```bash
git status
git branch
git log --oneline --graph --all
git remote -v
```

## მოკლე ახსნა

- `git init` — ქმნის ლოკალურ Git რეპოზიტორს.
- `git add` — ამზადებს ცვლილებებს commit-ისთვის.
- `git commit` — ინახავს ცვლილებებს ისტორიაში.
- `git push` — ატვირთავს ცვლილებებს GitHub-ზე.
- `git branch` — აჩვენებს/მართავს განშტოებებს.
- `git merge` — აერთიანებს ერთი branch-ის ცვლილებებს მეორეში.
- Merge conflict წარმოიქმნება, როცა Git ერთსა და იმავე მონაკვეთში ცვლილებებს ავტომატურად ვერ აერთიანებს.
