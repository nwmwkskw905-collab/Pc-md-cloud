name: macOS VM

on:
  workflow_dispatch:

jobs:
  macos-vm:
    runs-on: macos-15

    steps:
      - name: Verificar macOS
        run: |
          echo "===== SISTEMA ====="
          sw_vers
          echo ""
          echo "===== CPU ====="
          sysctl -n machdep.cpu.brand_string
          echo ""
          echo "===== MEMÓRIA ====="
          system_profiler SPHardwareDataType
          echo ""
          echo "===== XCODE ====="
          xcodebuild -version

      - name: Verificar ferramentas
        run: |
          echo "Swift:"
          swift --version

          echo "Git:"
          git --version

          echo "Ruby:"
          ruby --version

      - name: Listar simuladores iOS
        run: |
          xcrun simctl list devices available

      - name: Testar ambiente
        run: |
          mkdir -p ~/macos-test
          echo "VM macOS funcionando!" > ~/macos-test/status.txt
          cat ~/macos-test/status.txt
