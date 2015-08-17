# Maintainer: Guten Ye
# Contributor: mr_chapendi <mr.chapendi@gmail.com>

pkgname="rbwebkitgtk-git"
pkgver=20130218
pkgrel=2
pkgdesc="Ruby/GTK2 bindings for WebKit."
arch=("i686" "x86_64")
url="https://github.com/danlucraft/rbwebkitgtk"
license=("GPL")
depends=("ruby" "libwebkit" "hspell")
makedepends=("git" "ruby-pkgconfig")
provides=("rbwebkitgtk")
conflicts=("rbwebkitgtk")

_gitroot="git://github.com/danlucraft/rbwebkitgtk.git"
_gitname="rbwebkitgtk"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

	# 
	# BUILD HERE
	#

	sed -i 's/have_library("webkit-1.0")/have_library("webkitgtk-1.0")/' extconf.rb 

  ruby extconf.rb || return 1
  make || return 1
}

package() {
  cd "$srcdir/$_gitname-build"

  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
md5sums=()
