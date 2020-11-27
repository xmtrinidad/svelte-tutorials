## 11/27

I was following along with the tutorial and noticed the rollup config for section1 was outdated and I was getting build errors.

* Updated all packages to latest version
* Did some research on the rollup config
* The main change was that CSS bundling is done using the "rollup-plugin-css-only" package, rather than Svelte specific rollup settings
* The base rollup config now looks like this:

```javascript
import svelte from 'rollup-plugin-svelte';
import resolve from 'rollup-plugin-node-resolve';
import commonjs from 'rollup-plugin-commonjs';
import livereload from 'rollup-plugin-livereload';
import css from 'rollup-plugin-css-only'
import { terser } from 'rollup-plugin-terser';

const production = !process.env.ROLLUP_WATCH;

export default {
	input: 'src/main.js',
	output: {
		sourcemap: true,
		format: 'iife',
		name: 'app',
		file: 'public/bundle.js'
	},
	plugins: [
		css({ output: 'bundle.css' }),
		svelte({
			emitCss: true,
			compilerOptions: {
				// enable run-time checks when not in production
				dev: !production,
			}
		}),

		// If you have external dependencies installed from
		// npm, you'll most likely need these plugins. In
		// some cases you'll need additional configuration —
		// consult the documentation for details:
		// https://github.com/rollup/rollup-plugin-commonjs
		resolve(),
		commonjs(),

		// Watch the `public` directory and refresh the
		// browser on changes when not in production
		!production && livereload('public'),

		// If we're building for production (npm run build
		// instead of npm run dev), minify
		production && terser()
	]
};
```