<h1>MySQL</h1>
<p>MySQL adalah sistem manajemen basis data relasional (RDBMS) sumber terbuka yang banyak digunakan dan menawarkan berbagai fitur, alat, dan layanan untuk pergudangan data, analisis, pembelajaran mesin, dan banyak lagi. MariaDB adalah cabang MySQL yang populer dan stabil yang kompatibel dengan MySQL dan memiliki penyempurnaan dan fitur tambahan.</p>
<p><a href="https://nixos.wiki/wiki/Mysql">Dokumentasi</a></p>

<h3>Mempersiapkan</h3>
<p>Menyiapkan dan mengaktifkan daemon database Mysql (MariaDB)</p>
<p>Buka Folder .idx/dev.nix</p>
<p>Masukan script dibawah ini</p>
<pre>
  <code>
services.mysql = {
  enable = true;
  package = pkgs.mariadb;
};
  </code>
</pre>
<p>Perhatikan Script lengkapnya dibawah ini</p>
<pre>
  <code>
    # To learn more about how to use Nix to configure your environment
# see: https://developers.google.com/idx/guides/customize-idx-env
{pkgs}: {
  # Which nixpkgs channel to use.
  channel = "stable-23.11"; # or "unstable"
  # Use https://search.nixos.org/packages to find packages
  packages = [
    pkgs.php82
    pkgs.php82Packages.composer
    pkgs.nodejs_20
  ];

services.mysql = {
  enable = true;
  package = pkgs.mariadb;
};

  # Sets environment variables in the workspace
  env = {};
  idx = {
    # Search for the extensions you want on https://open-vsx.org/ and use "publisher.id"
    extensions = [
      # "vscodevim.vim"
    ];
    workspace = {
      # Runs when a workspace is first created with this `dev.nix` file
      onCreate = {
        # Example: install JS dependencies from NPM
        # npm-install = "npm install";
        # Open editors for the following files by default, if they exist:
        default.openFiles = [ "README.md" "resources/views/welcome.blade.php" ];
      };
      # To run something each time the workspace is (re)started, use the `onStart` hook
    };
    # Enable previews and customize configuration
    previews = {
      enable = true;
      previews = {
        web = {
          command = ["php" "artisan" "serve" "--port" "$PORT" "--host" "0.0.0.0"];
          manager = "web";
        };
      };
    };
  };
}

  </code>
</pre>

<h1>Pemeliharaan</h1>
<h3>Meningkatkan</h3>
<p>NixOS tidak akan berjalan mysql_upgradesecara otomatis untuk Anda setelah meng-upgrade ke versi utama yang baru, karena ini merupakan operasi yang "berbahaya" (dapat mengakibatkan kerusakan data) dan pengguna sangat disarankan (oleh MariaDB upstream) untuk mencadangkan database mereka sebelum menjalankannya mysql_upgrade.</p>
<pre>
  <code>mysqldump -u root -p --all-databases > alldb.sql</code>
</pre>
<br/>
<pre>
  <code>
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
  </code>
</pre>
<h1>PUDIN.MY.ID</h1>
