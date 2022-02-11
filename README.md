# Clean Code PHP

これは、[clean-code-php](https://github.com/yangweijie/clean-code-php)を日本語訳したものです。翻訳内容に不備があったり、無効なリンクなどがある場合には、issueあるいは、PRをお願いいたします。

「Clean Code PHP」の日本語訳については、他にも次のものがあります。

- [PHP: Clean Code (clean-code-php) 蜜柑薬](https://qiita.com/tadsan/items/c47eb327684530721e8a)
- [クリーンなPHPコードを書くためのガイド](https://qiita.com/rana_kualu/items/87ff47935f544441237c)

## 目次

  1. [はじめに](#はじめに)
  2. [変数](#変数)
     * [意味があり、発音可能な変数名を使用する](#意味があり、発音可能な変数名を使用する)
     * [同じタイプの変数には同じ語彙を使用する](#同じタイプの変数には同じ語彙を使用する)
     * [検索可能な名前を使用する(パート1)](#検索可能な名前を使用する-パート1)
     * [検索可能な名前を使用する(パート2)](#検索可能な名前を使用する-パート2)
     * [理解に役立つ変数を使用する](#理解に役立つ変数を使用する)
     * [深いネストを避けて、早期リターンを使用する(パート1)](#深いネストを避けて、早期リターンを使用する-パート1)
     * [深いネストを避けて、早期リターンを使用する(パート2)](#深いネストを避けて、早期リターンを使用する-パート2)
     * [メンタルマッピングを避ける](#メンタルマッピングを避ける)
     * [不要なコンテキストを避ける](#不要なコンテキストを避ける)
  3. [比較](#比較)
     * [厳密な比較を使用する](#厳密な比較を使用する)
     * [Null合体演算子](#Null合体演算子)
  4. [関数](#関数)
     * [短絡または条件の代わりにデフォルトの引数を使用する](#短絡または条件の代わりにデフォルトの引数を使用する)
     * [関数の引数 (2つ以下の引数が理想的)](#関数の引数-2つ以下の引数が理想的)
     * [関数名は何の処理を実行するかわかるようにする](#関数名は何の処理を実行するかわかるようにする)
     * [関数は1段階の抽象化のみにする](#関数は1段階の抽象化のみにする)
     * [関数の引数としてフラグを使用しない](#関数の引数としてフラグを使用しない)
     * [副作用を避ける](#副作用を避ける)
     * [グローバル関数に書き込まない](#グローバル関数に書き込まない)
     * [シングルトンパターンを使用しない](#シングルトンパターンを使用しない)
     * [条件文をカプセル化する](#条件文をカプセル化する)
     * [否定の条件文を避ける](#否定の条件文を避ける)
     * [条件文を避ける](#条件文を避ける)
     * [型チェックを避ける(パート1)](#型チェックを避ける-パート1)
     * [型チェックを避ける(パート2)](#型チェックを避ける-パート2)
     * [必要のないコードは取り除く](#必要のないコードは取り除く)
  5. [オブジェクトとデータ構造](#オブジェクトとデータ構造)
     * [オブジェクトのカプセル化を使用する](#オブジェクトのカプセル化を使用する)
     * [private/protectedなメンバーを持つオブジェクトを作成する](#private/protectedなメンバーを持つオブジェクトを作成する)
  6. [クラス](#クラス)
     * [継承よりコンポジションを優先する](#継承よりコンポジションを優先する)
     * [流れるようなインターフェイスを避ける](#流れるようなインターフェイスを避ける)
     * [finalクラスを優先する](#finalクラスを優先する)
  7. [SOLID原則](#SOLID原則)
     * [単一責任原則(SRP)](#単一責任原則-srp)
     * [オープン・クローズドの原則(OCP)](#オープン・クローズドの原則-OCP)
     * [リスコフの置換原則(LSP)](#リスコフの置換原則-LSP)
     * [インターフェイス分離の原則(ISP)](#インターフェイス分離の原則-ISP)
     * [依存性逆転の原則(DIP)](#依存性逆転の原則-DIP)
  8. [DRY原則(DRY)](#DRY原則-DRY)
  9.  [翻訳](#翻訳)

## はじめに

Robert C. Martinの著書である[*クリーンコード*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
のソフトウェア・エンジニアリングの原則をPHPに適用させたものです。

これはスタイルガイドではありません。リーダブルで再利用しやすく、リファクタリングしやすいソフトウェアをPHPで創り出すためのガイドです。

ここに書かれている全ての原則に厳密に従う必要はありませんし、普遍的に合意されているものでもありません。

あくまでガイドラインであり、それ以上のものではありませんが、*Clean Code*の著者による長年の集合的な経験をまとめたものです。

[clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)からインスピレーションを得ています。

多くの開発者はまだPHP5を使用していますが、このガイドラインのほとんどの例はPHP7.1以上を前提としています。

## 変数

### 意味があり、発音可能な変数名を使用する

**悪い例:**

```php
$ymdstr = $moment->format('y-m-d');
```

**良い例:**

```php
$currentDate = $moment->format('y-m-d');
```

**[⬆トップに戻る](#目次)**

### 同じタイプの変数には同じ名前を使用する

**悪い例:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**良い例:**

```php
getUser();
```

**[⬆トップに戻る](#目次)**

### 検索可能な名前を使用する (パート1)

コードを書くよりも多くのコードを読むことになります。そのため、私たちが書くコードは読みやすく、検索可能であることが大切です。

プログラムを理解するのに重要な変数名に適切な命名をしないことで、読みづらいコードになってしまいます。
変数名は、検索可能なものにしてください。

**悪い例:**

```php
// 448は何を表してるんだ？
$result = $serializer->serialize($data, 448);
```

**良い例:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### 検索可能な名前を使用する (パート2)

**悪い例:**

```php
class User
{
    // 7は何を表してるんだ？
    public $access = 7;
}

// 4は何を表してるんだ？
if ($user->access & 4) {
    // ...
}

// これは何をしている？
$user->access ^= 2;
```

**良い例:**

```php
class User
{
    public const ACCESS_READ = 1;

    public const ACCESS_CREATE = 2;

    public const ACCESS_UPDATE = 4;

    public const ACCESS_DELETE = 8;

    // デフォルトのUserには、read, create, updateの権限を持つ
    public $access = self::ACCESS_READ | self::ACCESS_CREATE | self::ACCESS_UPDATE;
}

if ($user->access & User::ACCESS_UPDATE) {
    // 処理を書く
}

// create権限を持たない
$user->access ^= User::ACCESS_CREATE;
```

**[⬆トップに戻る](#目次)**

### 理解に役立つ変数を使用する

**悪い例:**

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches[1], $matches[2]);
```

**悪くない例:**

以下はよりよい例ですが、それでも正規表現に大きく依存しています。

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

[, $city, $zipCode] = $matches;
saveCityZipCode($city, $zipCode);
```

**良い例:**

[サブパターン](https://www.php.net/manual/ja/regexp.reference.subpatterns.php)に名前をつけることで正規表現への依存を減らせます。

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(?<city>.+?)\s*(?<zipCode>\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

**[⬆トップに戻る](#目次)**

### 深いネストを避けて、早期リターンを使用する (パート1)

if-elseステートメントが多すぎると、読みづらいコードになることがあります。明瞭であることは、不明瞭であることより良いです。

**悪い例:**

```php
function isShopOpen($day): bool
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            }
            return false;
        }
        return false;
    }
    return false;
}
```

**良い例:**

```php
function isShopOpen(string $day): bool
{
    if (empty($day)) {
        return false;
    }

    $openingDays = ['friday', 'saturday', 'sunday'];

    return in_array(strtolower($day), $openingDays, true);
}
```

**[⬆トップに戻る](#目次)**

### 深いネストを避けて、早期リターンを使用する (パート2)

**悪い例:**

```php
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            }
            return 1;
        }
        return 0;
    }
    return 'Not supported';
}
```

**良い例:**

```php
function fibonacci(int $n): int
{
    if ($n === 0 || $n === 1) {
        return $n;
    }

    if ($n >= 50) {
        throw new Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```

**[⬆トップに戻る](#目次)**

### メンタルマッピングを避ける

コードを読む人に変数の意味を解読することを強制してはいけません。
変数の意味をはっきりさせてください。明瞭であることは、不明瞭であることより良いです。

**悪い例:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // $liは何を表してたんだっけ
    dispatch($li);
}
```

**良い例:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[⬆トップに戻る](#目次)**

### 不要なコンテキストを避ける

クラス名やオブジェクト名からわかることを、変数名で繰り返す必要はありません。

**悪い例:**

```php
class Car
{
    public $carMake;

    public $carModel;

    public $carColor;

    //...
}
```

**良い例:**

```php
class Car
{
    public $make;

    public $model;

    public $color;

    //...
}
```

**[⬆トップに戻る](#目次)**

## 比較

### 厳密な比較を使用する

[厳密な比較](https://www.php.net/manual/ja/language.operators.comparison.php)を使用してください。

**良くない例:**

単純な比較(緩やかな比較、曖昧な比較)では、文字列型を整数型に変換します。

```php
$a = '42';
$b = 42;

if ($a != $b) {
    // この式は常にスキップされます
}
```

`$a != $b`という比較は、`FALSE`を返しますが、実際には`TRUE`です!
文字列`42` は、整数値`42`とは異なります。

**良い例:**

厳密な比較では、型と値がともに比較されます。

```php
$a = '42';
$b = 42;

if ($a !== $b) {
    // この式は実行されます
}
```

`$a !== $b`という比較は、`TRUE`を返します。

**[⬆トップに戻る](#目次)**

### Null合体演算子

Null合体演算子は、[PHP7から導入された新しい演算子](https://www.php.net/manual/ja/migration70.new-features.php)です。
Null合体演算子`??`は、`isset()`と組み合わせて三項演算子を使用する必要がある一般的なケースの[糖衣構文](https://ja.wikipedia.org/wiki/%E7%B3%96%E8%A1%A3%E6%A7%8B%E6%96%87)として追加されました。Null合体演算子を使用すると、最初のオペランドが`null`でない場合にはそれを返します。`null`だった場合には、2番目のオペランドを返します。


**悪い例:**

```php
if (isset($_GET['name'])) {
    $name = $_GET['name'];
} elseif (isset($_POST['name'])) {
    $name = $_POST['name'];
} else {
    $name = 'nobody';
}
```

**良い例:**
```php
$name = $_GET['name'] ?? $_POST['name'] ?? 'nobody';
```

**[⬆トップに戻る](#目次)**

## 関数

### 短絡または条件の代わりにデフォルトの引数を使用する

**良くない例:**

`$breweryName`は`NULL`になる可能性があるため、これは適切ではありません。

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**悪くない例:**

この例は、先程の例よりも理解しやすいですが、変数の値を制御するほうがよいです。
This opinion is more understandable than the previous version, but it better controls the value of the variable.

```php
function createMicrobrewery($name = null): void
{
    $breweryName = $name ?: 'Hipster Brew Co.'; // `?:` はエルビス演算子
    // ...
}
```

**良い例:**

 [型宣言(タイプヒンティング)](https://www.php.net/manual/ja/language.types.declarations.php) を使用して、`$breweryName`が`NULL`にならないようにすることができます。

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**[⬆トップに戻る](#目次)**

### 関数の引数 (2つ以下の引数が理想的)

関数の引数の数を制限することは、非常に重要です。そうすることで、関数のテストが簡単になります。3つ以上の引数があると組み合わせの数が大きく増え、それぞれの引数に対する様々なケースをテストする必要がでてきます。

引数がないのが理想です。1つか2つであれば問題有りませんが、3つは避けた方がよいでしょう。
それ以上増える場合には、統合する必要があります。通常、2つより多い引数を指定する場合、その関数は多くのことを実行しようとしています。
そうでない場合、より高次のオブジェクトを引数とすることで事足りる場合も多くあります。

**悪い例:**

```php
class Questionnaire
{
    public function __construct(
        string $firstname,
        string $lastname,
        string $patronymic,
        string $region,
        string $district,
        string $city,
        string $phone,
        string $email
    ) {
        // ...
    }
}
```

**良い例:**

```php
class Name
{
    private $firstname;

    private $lastname;

    private $patronymic;

    public function __construct(string $firstname, string $lastname, string $patronymic)
    {
        $this->firstname = $firstname;
        $this->lastname = $lastname;
        $this->patronymic = $patronymic;
    }

    // getters ...
}

class City
{
    private $region;

    private $district;

    private $city;

    public function __construct(string $region, string $district, string $city)
    {
        $this->region = $region;
        $this->district = $district;
        $this->city = $city;
    }

    // getters ...
}

class Contact
{
    private $phone;

    private $email;

    public function __construct(string $phone, string $email)
    {
        $this->phone = $phone;
        $this->email = $email;
    }

    // getters ...
}

class Questionnaire
{
    public function __construct(Name $name, City $city, Contact $contact)
    {
        // ...
    }
}
```

**[⬆トップに戻る](#目次)**

### 関数名は何の処理を実行するかわかるようにする

**悪い例:**

```php
class Email
{
    //...

    public function handle(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// これは何を実行しているんだろう？ メッセージのハンドリング？ ファイル書き込みを行っているのだろうか？
$message->handle();
```

**良い例:**

```php
class Email
{
    //...

    public function send(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// わかりやすい
$message->send();
```

**[⬆トップに戻る](#目次)**

### 関数は1段階の抽象化のみにする

複数段階の抽象化がある場合、関数は通常、多くのことをやりすぎています。
関数を機能ごとに分解することで、再利用性の向上やよりテストしやすいコードになります。

**悪い例:**

```php
function parseBetterPHPAlternative(string $code): void
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**同じく悪い例:**

関数を分割していますが、`parseBetterPHPAlternative()`関数は、まだとても複雑で、テストしやすいものではありません。

```php
function tokenize(string $code): array
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer(array $tokens): array
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterPHPAlternative(string $code): void
{
    // `parseBetterPHPAlternative()`関数内で、それぞれの関数が実行されてしまっている
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**良い例:**

最善の解決策は、`parseBetterPHPAlternative()`関数の依存関係を取り除くことです。

```php
class Tokenizer
{
    public function tokenize(string $code): array
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify(array $tokens): array
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterPHPAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse(string $code): void
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[⬆トップに戻る](#目次)**

### 関数の引数として、フラグを使用しない

フラグは、関数が複数のことを実行することをユーザーに伝えます。1つの関数は1つのことを実行すべきです。ブール値に基づいて、実行内容が異なって来る場合には、関数を分割しましょう。

**悪い例:**

```php
function createFile(string $name, bool $temp = false): void
{
    if ($temp) {
        touch('./temp/' . $name);
    } else {
        touch($name);
    }
}
```

**良い例:**

```php
function createFile(string $name): void
{
    touch($name);
}

function createTempFile(string $name): void
{
    touch('./temp/' . $name);
}
```

**[⬆トップに戻る](#目次)**

### 副作用を避ける

関数は、値を受け取り、他の値を返す以外のことを行うと、副作用を引き起こします。副作用として、ファイルへの書き込み、グローバル変数の変更、または誤って赤の他人にあなたのお金を送金するなどのことが考えられます。

プログラムには副作用が時々必要です。上の例のように、ファイルへの書き込みが必要になる場合があります。したいことは、副作用の起こるプログラムを一元化することです。

特定のファイルに書き込む関数や、クラスをいくつも用意してはいけません。それを行うサービスは1つだけにすべきです。ただ1つです。

重要な点は、次に挙げるような一般的な落とし穴を避けることです。

- 構造のないオブジェクト間で状態を共有すること
- 何でも書き込める可変データ型を使用すること
- 副作用が派生する場所を一元化しないこと

これができれば、他の大多数のプログラマーより幸せになれます。

**悪い例:**

```php
// 次の関数によって参照されるグローバル変数
// このname変数を医療する他の関数がある場合、これは配列になり、動作しな可能性があります。
$name = 'Ryan McDermott';

function splitIntoFirstAndLastName(): void
{
    global $name;

    $name = explode(' ', $name);
}

splitIntoFirstAndLastName();

var_dump($name);
// ['Ryan', 'McDermott'];
```

**良い例:**

```php
function splitIntoFirstAndLastName(string $name): array
{
    return explode(' ', $name);
}

$name = 'Ryan McDermott';
$newName = splitIntoFirstAndLastName($name);

var_dump($name);
// 'Ryan McDermott';

var_dump($newName);
// ['Ryan', 'McDermott'];
```

**[⬆トップに戻る](#目次)**

### グローバル関数に書き込まない

グローバルスコープを汚染することは、多くの言語で悪い習慣です。なぜなら、他のライブラリと衝突する可能性があり、APIのユーザーは、本番環境で例外が発生するまでわかりらないためです。

設定状態をもつ配列が必要な場合について考えてみましょう。
`config（）`のようなグローバル関数を書くこともできますが、同じことをしようとした別のライブラリと衝突する可能性があります。

**悪い例:**

```php
function config(): array
{
    return [
        'foo' => 'bar',
    ];
}
```

**良い例:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get(string $key): ?string
    {
        // null coalescing operator
        return $this->configuration[$key] ?? null;
    }
}
```

設定を読み込み、`Configuration`のインスタンスを生成します。

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

そして今、アプリケーションで `Configuration`のインスタンスを使わなければなりません。

**[⬆トップに戻る](#目次)**

### シングルトンパターンを使用しない

シングルトンは、[アンチパターン](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%B3%E3%83%81%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3)です。
Brian Buttonから言い換えると、
 1. シングルトンは、一般的に**グローバル変数**として使用されますが、なぜそれほど悪いのですか？なぜなら、インターフェイスを介してそれらを公開するのではなく、コード内でアプリケーションの**依存関係を隠してしまう**からです。あるデータをあちこちに渡すのを避けるためにグローバルにすることは、[コードの臭い](https://ja.wikipedia.org/wiki/%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AE%E8%87%AD%E3%81%84)です。
 2. **自身のインスタンスの生成とライフサイクルを制御する**点から、[単一責任原則](#単一責任原則)に違反します。
 3. 本質的にコードの密結合を引き起こします。([結合度](https://ja.wikipedia.org/wiki/%E7%B5%90%E5%90%88%E5%BA%A6))これにより多くのケースで、**テスト時に仮のデータを用意するのが大変**になります。
 4. アプリケーションの寿命が尽きるまで、状態を持ち続けることになります。また、単体テストと相性の悪い**テストを順番に行う必要があるという状況に陥る可能性**があるためテストに影響があります。なぜなら、各単体テストは、互いに独立している必要があるためです。

[Misko Hevery](http://misko.hevery.com/about/)の[root of problemという記事](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/)が参考になるでしょう。

**悪い例:**

```php
class DBConnection
{
    private static $instance;

    private function __construct(string $dsn)
    {
        // ...
    }

    public static function getInstance(): self
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    // ...
}

$singleton = DBConnection::getInstance();
```

**良い例:**

```php
class DBConnection
{
    public function __construct(string $dsn)
    {
        // ...
    }

    // ...
}
```

`DBConnection`クラスのインスタンスを作成し、[DSN](https://www.php.net/manual/ja/pdo.construct.php#refsect1-pdo.construct-parameters)で構成します。

```php
$connection = new DBConnection($dsn);
```

そして今、アプリケーションで`DBConnection`のインスタンスを使わなければなりません。

**[⬆トップに戻る](#目次)**

### 条件文をカプセル化する

**悪い例:**

```php
if ($article->state === 'published') {
    // ...
}
```

**良い例:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[⬆トップに戻る](#目次)**

### 否定の条件文を避ける

**悪い例:**

```php
function isDOMNodeNotPresent(DOMNode $node): bool
{
    // ...
}

if (! isDOMNodeNotPresent($node)) {
    // ...
}
```

**良い例:**

```php
function isDOMNodePresent(DOMNode $node): bool
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[⬆トップに戻る](#目次)**

### 条件文を避ける

これは、不可能なことのように思われます。これを最初に聞いた時、ほとんどの人はこう言います。
「`if`ステートメントなしで、どうすればいいんだ？」と。
答えは、多くのケースで、ポリモーフィズムを使用して同じタスクを達成することができる、ということです。

二番目の質問は通常、「なぜポリモーフィズムを使用する必要があるんだ？」です。
答えは、すでに学んだ以前のclean codeの概念の、関数は1つのことを実行すべき、というものです。`if`ステートメントを持つクラスと関数がある場合、関数が複数のことを実行することをユーザーに伝えます。ただ1つのことだけ、ということを覚えておいてください。

**悪い例:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**良い例:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude(): int;
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

**[⬆トップに戻る](#目次)**

### 型チェックを避ける (パート1)

PHPは型指定されていません。そのため、関数は任意の型の引数をとることができます。
あらゆる型の可能性があることから、型のチェックを関数内で行いたくなることがあります。
これをさける方法は多くあります。まず考慮すべきことは、一貫性のあるAPIです。

**悪い例:**

```php
function travelToTexas($vehicle): void
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->pedalTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**良い例:**

```php
function travelToTexas(Vehicle $vehicle): void
{
    $vehicle->travelTo(new Location('texas'));
}
```

**[⬆トップに戻る](#目次)**

### 型チェックを避ける (パート2)

文字列や整数、配列などの基本的なプリミティブを使用していて、PHP7以降を使用していて、ポリモーフィズムを使用できないという場合においても、
型チェックが必要であれば、[型宣言](https://www.php.net/manual/ja/language.types.declarations.php)やstrictモードを検討してみてください。
それにより、標準のPHP構文に加えて、静的型付けをを行えます。
手動での型チェックの問題は、可読性の低下を補わない偽物の「型安全」のために多くの余分なコードが必要になることです。
PHPをクリーンに保ち、優れたテストを作成し、優れたコードレビューを行いましょう。そうでなければ、PHPの厳密な型宣言やstrictモードを使用してすべてのコードを実行しましょう。

**悪い例:**

```php
function combine($val1, $val2): int
{
    if (! is_numeric($val1) || ! is_numeric($val2)) {
        throw new Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**良い例:**

```php
function combine(int $val1, int $val2): int
{
    return $val1 + $val2;
}
```

**[⬆トップに戻る](#目次)**

### 必要のないコードは取り除く

実行されることのないコードは、重複しているコードと同じくらい悪いです。コードの中にそれをおいておく理由はありません。呼び出されない場合は、削除してください。
それでも必要な場合には、バージョン履歴を利用しましょう。

**悪い例:**

```php
function oldRequestModule(string $url): void
{
    // ...
}

function newRequestModule(string $url): void
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**良い例:**

```php
function requestModule(string $url): void
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[⬆トップに戻る](#目次)**


## オブジェクトとデータ構造

### オブジェクトのカプセル化を使用する

PHPのメソッドには、`public`、 `protected`、`private`のキーワードを設定することができます。
これを使用して、オブジェクトのプロパティの変更を制御できます。

* オブジェクトのプロパティを取得する以上のことをしたい場合には、コード内の全てのアクセサを検索し、変更する必要はありません。
* `set`を実行するときに、検証を簡単に実行できます。
* 内部表現をカプセル化します。
* 取得および、設定時にログとエラー処理を簡単に追加できます。
* このクラスを継承すると、デフォルトの機能をオーバーライドできます。
* オブジェクトのプロパティを遅延ロードできます。例えば、サーバーからオブジェクトを取得できます。

さらに、これは[オープン・クローズド](#オープン・クローズドの原則-OCP)原則の一部です。

**悪い例:**

```php
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->balance -= 100;
```

**良い例:**

```php
class BankAccount
{
    private $balance;

    public function __construct(int $balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdraw(int $amount): void
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function deposit(int $amount): void
    {
        $this->balance += $amount;
    }

    public function getBalance(): int
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// 靴を購入
$bankAccount->withdraw($shoesPrice);

// 残高を取得
$balance = $bankAccount->getBalance();
```

**[⬆トップに戻る](#目次)**

### private/protectedなメンバーを持つオブジェクトを作成する

* `public`メソッドとプロパティは、変更にたいして最も危険です。なぜなら、外部のコードは簡単にそれらに依存する可能性があり、どのコードが依存するかを制御できないためです。
* `protected`修飾子は、すべての子クラスのスコープで使用できるため、publicクラスと同じくらい危険です。これは事実上、publicとprotectedの違いは、アクセスメカニズムのみにあることを意味しますが、カプセル化の保証は同じままです。**クラスの変更は、すべての子孫クラスにとって危険です。**
* `private`修飾子は、コードが**単一クラスの内部のみ変更する危険性**があることを保証します。(変更しても安全であり、[Jenga effect](http://www.urbandictionary.com/define.php?term=Jengaphobia&defid=2494196)はありません。)

それゆえ、デフォルトでは`private`を使用し、外部のクラスへアクセスを提供する必要がある場合に`public/protected`を使用してください。

詳細については、[Fabien Potencier](https://github.com/fabpot)によって書かれた[Pragmatism over Theory: Protected vs Private](http://fabien.potencier.org/pragmatism-over-theory-protected-vs-private.html)を読んでみてください。

**悪い例:**

```php
class Employee
{
    public $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }
}

$employee = new Employee('John Doe');
// Employee name: John Doe
echo 'Employee name: ' . $employee->name;
```

**良い例:**

```php
class Employee
{
    private $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function getName(): string
    {
        return $this->name;
    }
}

$employee = new Employee('John Doe');
// Employee name: John Doe
echo 'Employee name: ' . $employee->getName();
```

**[⬆トップに戻る](#目次)**

## クラス

### 継承よりコンポジションを優先する

Gang of Four(GOF)の[*デザインパターン*](https://en.wikipedia.org/wiki/Design_Patterns)で有名に述べられているように、
可能な場合には、継承よりもコンポジションを優先する必要があります。継承を使用する正当な理由と、コンポジションを使用する正当な理由はたくさんあります。
この格言の要点は、あなたの心が本能的に継承を使いたがっている場合に、コンポジションが問題をよりよくモデル化できないかを考えた方がよい、ということです。場合によっては、可能です。

それなら「いつ継承を使うべきなのか？」と疑問に思われるかもしれません。これは、手元の問題によりますが、以下は継承がコンポジションよりも理にかなっている場合のリストです。

1. 継承が、「has-a」関係ではなく、「is-a」関係を表している(Human->Animal vs. User->UserDetails)
2. 基底クラスのコードを再利用できる(人間は、全ての動物と同じように動くことができる)
3. 基底クラスを変更して、派生クラスにグローバルな変更を加えたい。(移動する全ての動物のカロリー消費量を変更する。)

**悪い例:**

```php
class Employee
{
    private $name;

    private $email;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}

// 従業員がtaxDataを「持っている」ため悪い
// EmployeeTaxDataはEmployeeの型ではない

class EmployeeTaxData extends Employee
{
    private $ssn;

    private $salary;

    public function __construct(string $name, string $email, string $ssn, string $salary)
    {
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}
```

**良い例:**

```php
class EmployeeTaxData
{
    private $ssn;

    private $salary;

    public function __construct(string $ssn, string $salary)
    {
        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}

class Employee
{
    private $name;

    private $email;

    private $taxData;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData(EmployeeTaxData $taxData): void
    {
        $this->taxData = $taxData;
    }

    // ...
}
```

**[⬆トップに戻る](#目次)**

### 流れるようなインターフェイスを避ける

[流れるようなインターフェイス](https://en.wikipedia.org/wiki/Fluent_interface)とは、[メソッドチェーン](https://en.wikipedia.org/wiki/Method_chaining)を用いて、ソースコードの可読性を高めることを目的としたオブジェクト指向APIのことです。

ビルダーオブジェクトのように、このパターンがコードの冗長性をへらす場合もありますが(例えば、[PHPUnit Mock Builder](https://phpunit.de/manual/current/en/test-doubles.html) や [Doctrine Query Builder](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/query-builder.html)などのように)、多くの場合には以下のような代償が必要になります。

1. [カブセル化](https://ja.wikipedia.org/wiki/%E3%82%AB%E3%83%97%E3%82%BB%E3%83%AB%E5%8C%96)を壊す
2. [デコレータ](https://ja.wikipedia.org/wiki/Decorator_%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3)を壊す
3. テストスイートで[モック](https://ja.wikipedia.org/wiki/%E3%83%A2%E3%83%83%E3%82%AF%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)するのは難しい
4. コミットの差分が読みにくくなる

詳細については、[Marco Pivetta](https://github.com/Ocramius)によって書かれた[fluent-interfaces-are-evil](https://ocramius.github.io/blog/fluent-interfaces-are-evil/)を読んでみてください。

**悪い例:**

```php
class Car
{
    private $make = 'Honda';

    private $model = 'Accord';

    private $color = 'white';

    public function setMake(string $make): self
    {
        $this->make = $make;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setModel(string $model): self
    {
        $this->model = $model;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setColor(string $color): self
    {
        $this->color = $color;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = (new Car())
    ->setColor('pink')
    ->setMake('Ford')
    ->setModel('F-150')
    ->dump();
```

**良い例:**

```php
class Car
{
    private $make = 'Honda';

    private $model = 'Accord';

    private $color = 'white';

    public function setMake(string $make): void
    {
        $this->make = $make;
    }

    public function setModel(string $model): void
    {
        $this->model = $model;
    }

    public function setColor(string $color): void
    {
        $this->color = $color;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = new Car();
$car->setColor('pink');
$car->setMake('Ford');
$car->setModel('F-150');
$car->dump();
```

**[⬆トップに戻る](#目次)**

### finalクラスを優先する

`final`キーワードは、可能な限り使用すべきです。

1. 制御されていない継承チェーンを防ぎます。
2. [コンポジション](#継承よりコンポジションを優先する)を奨励します。
3. [単一責任原則](#単一責任原則)を奨励します。
4. 保護されたクラスにアクセスするためにクラスを拡張する代わりに、publicメソッドを使用することを奨励します。
5. クラスを使用するアプリケーションを壊すことなく、コードを変更できます。

唯一の条件は、クラスがインターフェイスを実装する必要があり、他のpublicメソッドが定義されていないことです。

詳細については、[Marco Pivetta (Ocramius)](https://ocramius.github.io/)によって書かれた[when-to-declare-classes-final](https://ocramius.github.io/blog/when-to-declare-classes-final/)を読んでみてください。

**悪い例:**

```php
final class Car
{
    private $color;

    public function __construct($color)
    {
        $this->color = $color;
    }

    /**
     * @return string The color of the vehicle
     */
    public function getColor()
    {
        return $this->color;
    }
}
```

**良い例:**

```php
interface Vehicle
{
    /**
     * @return string The color of the vehicle
     */
    public function getColor();
}

final class Car implements Vehicle
{
    private $color;

    public function __construct($color)
    {
        $this->color = $color;
    }

    public function getColor()
    {
        return $this->color;
    }
}
```

**[⬆トップに戻る](#目次)**

## SOLID原則

**SOLID**は、Robert Martinが名付けた5つの原則の頭文字をとって、Michael Feathersが提唱したニーモニックです。

 * [S: 単一責任原則(SRP)](#単一責任原則-SRP)
 * [O: オープン・クローズドの原則(OCP)](#オープン・クローズドの原則-OCP)
 * [L: リスコフの置換原則(LSP)](#リスコフの置換原則-LSP)
 * [I: インターフェイス分離の原則(ISP)](#インターフェイス分離の原則-ISP)
 * [D: 依存性逆転の原則(DIP)](#依存性逆転の原則-DIP)

### 単一責任原則 (SRP)

クリーンコードで記載されているように、「クラスが変更される理由は複数あってはなりません」。飛行機でスーツケースを1つしか持って行けない時のように、クラスに多くの機能を詰め込みたくなるものです。
この場合の問題点は、クラスが概念的にまとまらず、変更する理由をたくさん与えてしまうことです。クラスを変更する回数を最小限にすることが大切です。
なぜなら、あまりに多くの機能が1つのクラスに入っていて、その一部を変更した場合、それがコード内の他の依存モジュールにどのような影響を与えるか理解し難くなるからです。

**悪い例:**

```php
class UserSettings
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function changeSettings(array $settings): void
    {
        if ($this->verifyCredentials()) {
            // ...
        }
    }

    private function verifyCredentials(): bool
    {
        // ...
    }
}
```

**良い例:**

```php
class UserAuth
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function verifyCredentials(): bool
    {
        // ...
    }
}

class UserSettings
{
    private $user;

    private $auth;

    public function __construct(User $user)
    {
        $this->user = $user;
        $this->auth = new UserAuth($user);
    }

    public function changeSettings(array $settings): void
    {
        if ($this->auth->verifyCredentials()) {
            // ...
        }
    }
}
```

**[⬆トップに戻る](#目次)**

### オープン・クローズドの原則 (OCP)

Bertrand Meyerが述べているように、「ソフトウェアエンティティ(クラス、モジュール、関数など)は、拡張のためにオープンである必要がありますが、変更のためにクローズドである必要があります。」
どういう意味でしょう。この原則は、基本的にユーザーに既存のコードを変更せずに新しい機能を追加できるようにする必要があることを示しています。

**悪い例:**

```php
abstract class Adapter
{
    protected $name;

    public function getName(): string
    {
        return $this->name;
    }
}

class AjaxAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'ajaxAdapter';
    }
}

class NodeAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'nodeAdapter';
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        $adapterName = $this->adapter->getName();

        if ($adapterName === 'ajaxAdapter') {
            return $this->makeAjaxCall($url);
        } elseif ($adapterName === 'httpNodeAdapter') {
            return $this->makeHttpCall($url);
        }
    }

    private function makeAjaxCall(string $url): Promise
    {
        // request and return promise
    }

    private function makeHttpCall(string $url): Promise
    {
        // request and return promise
    }
}
```

**良い例:**

```php
interface Adapter
{
    public function request(string $url): Promise;
}

class AjaxAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class NodeAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        return $this->adapter->request($url);
    }
}
```

**[⬆トップに戻る](#目次)**

### リスコフの置換原則 (LSP)

これは、非常に単純な概念の恐ろしい単語です。正式には、「SがTのサブタイプであれば、T型のオブジェクトは、そのプログラムの望ましい特性（正しさ、実行されたタスクなど）を一切変更することなく、T型のオブジェクトをS型のオブジェクトで置き換え可能（すなわち、S型のオブジェクトがT型のオブジェクトの代わりになることがある）」という恐ろしい定義です。

これについての最も良い説明は、親クラスと子クラスがあれば、親クラスと小クラスを入れ替わっても間違った結果にならない、というものです。これでもまだわかりにくいかもしれませんので、古典的な正方形と長方形の例を見てみましょう。
数学的には正方形は長方形なのですが、継承による「is-a」の関係を使ってモデル化するとすぐに問題が生じます。


**悪い例:**

```php
class Rectangle
{
    protected $width = 0;

    protected $height = 0;

    public function setWidth(int $width): void
    {
        $this->width = $width;
    }

    public function setHeight(int $height): void
    {
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square extends Rectangle
{
    public function setWidth(int $width): void
    {
        $this->width = $this->height = $width;
    }

    public function setHeight(int $height): void
    {
        $this->width = $this->height = $height;
    }
}

function printArea(Rectangle $rectangle): void
{
    $rectangle->setWidth(4);
    $rectangle->setHeight(5);

    // BAD: Will return 25 for Square. Should be 20.
    echo sprintf('%s has area %d.', get_class($rectangle), $rectangle->getArea()) . PHP_EOL;
}

$rectangles = [new Rectangle(), new Square()];

foreach ($rectangles as $rectangle) {
    printArea($rectangle);
}
```

**良い例:**

最良の方法は、四角形を分離し、両方の形状に対してより一般的なサブタイプを割り当てることです。

正方形と長方形の見かけの類似性にもかかわらず、それらは異なっています。正方形はひし形と多くの共通点があり、長方形には平方四辺形がありますが、これらはサブタイプではありません。
正方形、長方形、ひし形、平行四辺形は、形は似ていますが、独自の特性をもつ別々の形状をしています。

```php
interface Shape
{
    public function getArea(): int;
}

class Rectangle implements Shape
{
    private $width = 0;
    private $height = 0;

    public function __construct(int $width, int $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square implements Shape
{
    private $length = 0;

    public function __construct(int $length)
    {
        $this->length = $length;
    }

    public function getArea(): int
    {
        return $this->length ** 2;
    }
}

function printArea(Shape $shape): void
{
    echo sprintf('%s has area %d.', get_class($shape), $shape->getArea()).PHP_EOL;
}

$shapes = [new Rectangle(4, 5), new Square(5)];

foreach ($shapes as $shape) {
    printArea($shape);
}
```

**[⬆トップに戻る](#目次)**

### インターフェイス分離の原則 (ISP)

ISPでは、「クライアントが使用しないインターフェースに依存ｎすることを強制されるべきではない」と述べています。

この原則を示す良い例として、大きな設定オブジェクトを必要とするクラスを見てみましょう。クライアントに膨大な量のオプションの設定を要求しないことは、ほとんどの場合、すべての設定を必要としないので有益です。オプションにすることで「太いインターフェース」を持つことを防ぐことができます。

**悪い例:**

```php
interface Employee
{
    public function work(): void;

    public function eat(): void;
}

class HumanEmployee implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        // ...... eating in lunch break
    }
}

class RobotEmployee implements Employee
{
    public function work(): void
    {
        //.... working much more
    }

    public function eat(): void
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

**良い例:**

全ての労働者が従業員であるわけではなく、すべての従業員が労働者です。


```php
interface Workable
{
    public function work(): void;
}

interface Feedable
{
    public function eat(): void;
}

interface Employee extends Feedable, Workable
{
}

class HumanEmployee implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        //.... eating in lunch break
    }
}

// robot can only work
class RobotEmployee implements Workable
{
    public function work(): void
    {
        // ....working
    }
}
```

**[⬆トップに戻る](#目次)**

### 依存性逆転の原則 (DIP)

この原則は、2つの本質的なことを述べています。
1. 高位のモジュールは、低位のモジュールに低位のモジュールに依存すべきではありません。どちらも抽象化されたものに依存すべきです。
2. 抽象化されたものは具体的なものに依存するべきではありません。具体的なものは、抽象化されたものに依存すべきです。

最初は理解しにくいかもしれませんが、PHPフレームワーク(Symfonyなど)を使っている人であれば、この原則の実装を、依存性注入(DI)という形で見たことがあると思います。
両者は同一の概念ではありませんが、DIPは高レベルのモジュールがその低レベルのモジュールの詳細を知り、設定することを防ぎます。それは、DIによって実現できます。
これによる大きな利点は、モジュール間の結合を減らすことができることです。結合はコードのリファクタリングが難しくなるため、非常に悪い開発パターンです。

**悪い例:**

```php
class Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot extends Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**良い例:**

```php
interface Employee
{
    public function work(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**[⬆トップに戻る](#目次)**

## DRY原則 (DRY)

[DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)の原則を守るようにしてください。
コードの重複を極力避けてください。重複したコードは、ロジックを変更する必要がある場合に、変更する場所が複数になるので好ましくありません。

例えば、あなたがレストランを経営していて、トマト、タマネギ、ニンニク、スパイスなどの在庫を管理しているとします。もし、複数の在庫リストがあれば、トマトを使った料理を提供するときに、すべてのリストを更新しなければなりません。リストが1つしかない場合は、更新する場所は1つだけです。

コードが重複するのは、2つ以上の微妙に異なるコードを持っているからです。そして、その違いのために、ほとんど同じことをするのに2つ以上の別々の関数を用意しなければなりません。
重複するコードを削除するということは、このような異なるものの集合をたった一つの関数／モジュール／クラスで扱えるような抽象化を作るということです。

抽象化を正しく行うことは非常に重要です。そのためには、[クラス](#クラス)のセクションで説明したSOLIDの原則に従う必要があります。間違った抽象化は、重複したコードよりも悪いので注意が必要です。とはいえ、良い抽象化ができるのであれば、それを実行しましょう。そうでなければ、1つのことを変更するたびに、複数の場所を更新することになるでしょう。

**悪い例:**

```php
function showDeveloperList(array $developers): void
{
    foreach ($developers as $developer) {
        $expectedSalary = $developer->calculateExpectedSalary();
        $experience = $developer->getExperience();
        $githubLink = $developer->getGithubLink();
        $data = [$expectedSalary, $experience, $githubLink];

        render($data);
    }
}

function showManagerList(array $managers): void
{
    foreach ($managers as $manager) {
        $expectedSalary = $manager->calculateExpectedSalary();
        $experience = $manager->getExperience();
        $githubLink = $manager->getGithubLink();
        $data = [$expectedSalary, $experience, $githubLink];

        render($data);
    }
}
```

**良い例:**

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        $expectedSalary = $employee->calculateExpectedSalary();
        $experience = $employee->getExperience();
        $githubLink = $employee->getGithubLink();
        $data = [$expectedSalary, $experience, $githubLink];

        render($data);
    }
}
```

**より良い例:**

コンパクトにまとめるとより良いです。

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        render([$employee->calculateExpectedSalary(), $employee->getExperience(), $employee->getGithubLink()]);
    }
}
```

**[⬆トップに戻る](#目次)**

## 翻訳

他の言語での翻訳:

* :cn: **Chinese:**
   * [php-cpm/clean-code-php](https://github.com/php-cpm/clean-code-php)
* :ru: **Russian:**
   * [peter-gribanov/clean-code-php](https://github.com/peter-gribanov/clean-code-php)
* :es: **Spanish:**
   * [fikoborquez/clean-code-php](https://github.com/fikoborquez/clean-code-php)
* :brazil: **Portuguese:**
   * [fabioars/clean-code-php](https://github.com/fabioars/clean-code-php)
   * [jeanjar/clean-code-php](https://github.com/jeanjar/clean-code-php/tree/pt-br)
* :thailand: **Thai:**
   * [panuwizzle/clean-code-php](https://github.com/panuwizzle/clean-code-php)
* :fr: **French:**
   * [errorname/clean-code-php](https://github.com/errorname/clean-code-php)
* :vietnam: **Vietnamese:**
   * [viethuongdev/clean-code-php](https://github.com/viethuongdev/clean-code-php)
* :kr: **Korean:**
   * [yujineeee/clean-code-php](https://github.com/yujineeee/clean-code-php)
* :tr: **Turkish:**
   * [anilozmen/clean-code-php](https://github.com/anilozmen/clean-code-php)
* :iran: **Persian:**
   * [amirshnll/clean-code-php](https://github.com/amirshnll/clean-code-php)
* :bangladesh: **Bangla:**
   * [nayeemdev/clean-code-php](https://github.com/nayeemdev/clean-code-php)
* :egypt: **Arabic:**
   * [ahmedjoda/clean-code-php](https://github.com/ahmedjoda/clean-code-php)

**[⬆トップに戻る](#目次)**
