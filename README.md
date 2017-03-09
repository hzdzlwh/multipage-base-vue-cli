# a

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

# 构建多页面应用
# 1，在src下新建modules文件夹，modules文件夹下的每一个文件夹都一个页面，里面包含一个js文	 件，一个html文件，一个vue文件
# 2，修改build下的utils.js文件，增加如下：
	 var glob = require('glob');  //glob模块，用于读取webpack入口目录文件,需要npm安装
	 在文件末尾加入如下代码：
	 exports.getEntries = function (globPath) {
	  var entries = {},
	    basename, tmp, pathname;

	  glob.sync(globPath).forEach(function (entry) {
	    basename = path.basename(entry, path.extname(entry), 'router.js');
	    tmp = entry.split('/').splice(-3);
	    pathname = tmp.splice(0, 1) + '/' + basename; // 正确输出js和html的路径
	    entries[pathname] = entry;
	    //entries[basename] = entry;
	  });
	  console.log(entries)
	  /************************************************************
	  	{
	  		'modules/login': './src/modules/login/login.js',
	  		'modules/welcome': './src/modules/welcome/welcome.js'
	  	}
	  	{
	  		'modules/login': './src/modules/login/login.html',
	  		'modules/welcome': './src/modules/welcome/welcome.html'
	  	}
	  ***************************************************************/
	  return entries;
	}
# 3, 修改webpack.base.conf.js,如下：entry: utils.getEntries('./src/modules/**/*.js'),
# 4，修改webpack.dev.conf.js, 增加如下：
	 var pages = utils.getEntries('./src/modules/**/*.html')
		for (var pathname in pages) {
		  // 配置生成的html文件，定义路径等
		  var conf = {
		    filename: pathname + '.html',
		    template: pages[pathname],   // 模板路径
		    inject: true              // js插入位置

		  };
		 
		  if (pathname in module.exports.entry) {
		    conf.chunks = ['vendors', pathname];
		    conf.hash = true;
		  }
		  conf.chunks.push('manifest'); //加载公共chunks
		  conf.chunks.push('vendor');   //加载公共chunks
		  
		  module.exports.plugins.push(new HtmlWebpackPlugin(conf));
		}
	把原来的module.exports.plugins下的new HtmlWebpackPlugin()注释掉，用上面的
# 5，修改webpack.prod.conf.js,增加如下：
	 var pages = utils.getEntries('./src/modules/**/*.html')
		for (var pathname in pages) {
		  // 配置生成的html文件，定义路径等
		  var conf = {
		    filename: pathname + '.html',
		    template: pages[pathname],   // 模板路径
		    inject: true              // js插入位置

		  };
		  if (pathname in webpackConfig.entry) {
		    conf.chunks = ['vendors', pathname];
		    conf.hash = true;
		  }
		  conf.chunks.push('manifest');
		  conf.chunks.push('vendor');

		  webpackConfig.plugins.push(new HtmlWebpackPlugin(conf));
		}

		module.exports = webpackConfig
	把原来的new HtmlWebpackPlugin()注释。