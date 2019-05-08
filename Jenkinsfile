stage("Build and Publish") {
  node {
    ws('workspace/d2l-ko') {
      checkout scm
      sh "git submodule update --init"
      sh "build/utils/sanity_check.sh"
      sh "build/utils/clean_build.sh"
      sh "conda env update -f build/env.yml"
      sh "conda activate d2l-ko-build"
      sh "pip uninstall mxnet-cu92"
      sh "build/utils/build_html.sh ko"
      sh "build/utils/build_pdf.sh ko"
      sh "build/utils/build_pkg.sh ko"
      if (env.BRANCH_NAME == 'master') {
        sh "build/utils/publish_website.sh ko"
      }
	}
  }
}
