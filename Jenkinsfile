 node ('windows-release'){
  stage 'Checkout Client'
  git url: "https://github.com/keybase/client.git", branch: 'zanderz/jenkins=2016.11.11'
  stage 'Checkout KBFS'
  git url: "https://github.com/keybase/kbfs.git"
  stage 'Checkout go-updater'
  git url: "https://github.com/keybase/go-updater.git"  
  stage 'Checkout release'
  git url: "https://github.com/keybase/release.git"    
//  if not EXIST %WORKSPACE%\bin mkdir %WORKSPACE%\bin
  bat '''
    if EXIST src\github.com\keybase\client\desktop\release rmdir /q /s src\github.com\keybase\client\desktop\release
    :: Ongoing issues trying to build UI 
    git checkout src\github.com\keybase\client\shared
    git checkout src\github.com\keybase\client\desktop\shared
  '''
  stage 'Build Client'
  bat '"%ProgramFiles(x86)%\\Microsoft Visual Studio 14.0\\vc\\bin\\vcvars32.bat" && src\github.com\keybase\client\packaging\windows\build_prerelease.cmd' 
  stage 'Build UI'
  bat 'pushd  %GOPATH%\src\github.com\keybase\client\desktop && npm i'
  bat 'buildui.bat'
  stage 'Build Installer'
  bat '"%ProgramFiles(x86)%\\Microsoft Visual Studio 14.0\\vc\\bin\\vcvars32.bat" && src\github.com\keybase\client\packaging\windows\doinstaller_wix.cmd'
}

