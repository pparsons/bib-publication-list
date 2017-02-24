var fs = require('fs'),
  path = require('path'),
  jsmin = require('jsmin').jsmin

task('concat', [], function () {
  var files = ('lib/BibTex-0.1.2.js lib/jquery.dataTables.min.js '
              + 'src/bib-publication-list.js').split(' '),
      filesLeft = files.length,
      pathName = '.',
      outFile = fs.openSync('build/bib-list.js', 'w+');

  files.forEach(function(fileName) {
    var fileName = path.join(pathName, fileName),
        contents = fs.readFileSync(fileName);
    console.log('Read: ' + contents.length + ', written: ' + fs.writeSync(outFile, contents.toString()));
  });
  fs.closeSync(outFile);
});

task('clean', [], function() {
  fs.unlinkSync('build/bib-list.js');
  fs.unlinkSync('build/bib-list-min.js');
});

task('minify', ['concat'], function() {
  var code = fs.readFileSync('build/bib-list.js'),
      outFile = fs.openSync('build/bib-list-min.js', 'w+');
  console.log('Read: ' + code.length + ', written: ' + fs.writeSync(outFile, jsmin(code.toString())));
  fs.closeSync(outFile);
});

desc('Main build task');
task('build', ['concat', 'minify'], function() {});
task('rebuild', ['clean', 'build'], function() {});
