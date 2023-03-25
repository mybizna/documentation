# How to Participate

```
git clone --depth 1 https://github.com/mybizna/mybizna

cd mybizna

git submodule init
git submodule update
git submodule foreach 'git fetch origin; git checkout $(git rev-parse --abbrev-ref HEAD); git reset --hard origin/$(git rev-parse --abbrev-ref HEAD); git submodule update --recursive; git clean -dfx'

cp .env.example .env

composer install
composer dump-autoload -o

php artisan automigrator:migrate

php artisan tinker
$user = new App\Models\User();
$user->password = Hash::make('johndoe_2023');
$user->email = 'johndoe@johndoe.com';
$user->name = 'John Doe';
$user->username = 'johndoe';
$user->phone = '0723232323';
$user->save();

php artisan mybizna:dataprocessor

php artisan vendor:publish --provider="Mybizna\Assets\Providers\MybiznaAssetsProvider"

php artisan key:generate

php artisan serve

```

If you want to run a build for JS and CSS Resources from scratch.

```

npm install
npm run build

```
