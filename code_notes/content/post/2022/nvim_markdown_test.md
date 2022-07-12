---
title: "nvim for writing in markdown"
date: 2022-07-12T08:01:32-05:00
draft: false
author: "Jesus"
tags: ["nvim", "markdown"]
---

NeoVim or `nvim` is a text editor based on the terminal,
it is used to edit plain text or even for programming.
In my case I decided to set up my `nvim` for writting in markdown.
To have this configuration it is neccesary to cofig NeoVim.  

This modification were based on two sources: 
- jdhao webpage (She is a machine learning engineer):
	- [Markdown Writing and previewing in NeoVim - A complete Guide](https://jdhao.github.io/2019/01/15/markdown_edit_preview_nvim/)
- Nicolas Schourmann (Programmer, New Zeland): 
	- [Vim, aumenta tu velocidad de desarrollo](https://www.udemy.com/course/vim-aumenta-tu-velocidad-de-desarrollo/)

Following jdhao tutorial + Nicolar Shourman course you can learn to customize your nvim enviroment and even you will learn to use the nvim editor. 

- What is nvim
- How to use nvim
- How to install pluggins 
- Custumize youy nvim for markdwon writing

## My nvim config file ##

The easy way to tune nvim for Markdown writing is to implement my confi file. Here you need to find the `init.vim` located in the `.config/nvim` folder. To acces this file you should go to nvim folder and there write `nvim init.vim`  

Here I share my configuration file, pay attention to the following plugins: 

- **jiangmiao/auto-pairs**: auto complete parenthesus (  ),{  },[  ]
- junegunn/goyo.vim (this shows a focus mode for writing)
- SirVer/ultisnips (add snippets to accelerate Markdown writing)
- honza/vim-snippets (add snippets to accelerate Markdown writing)
- plasticboy/vim-markdown (Very important, add highlight and conceal Markdown)
- iamcco/markdown-preview.nvim (You can preview Markdown file in local)

```nvim

set number
set clipboard=unnamed
set tabstop=4
set shiftwidth=4
set smartindent
set mouse=a
syntax enable
set showcmd
set encoding=utf-8 
set showmatch
set relativenumber

call plug#begin('~/.vim/plugged')

" Gruvbox Themes
Plug 'sainnhe/gruvbox-material'
" Easy motion - Jump inside text

Plug 'easymotion/vim-easymotion'

" LSP 
Plug 'neovim/nvim-lspconfig'
Plug 'nvim-lua/completion-nvim'
Plug 'neoclide/coc.nvim', {'branch': 'master', 'do': 'yarn install --frozen-lockfile'}

"  Indent lines 
Plug 'Yggdroot/indentLIne'

" Airline (TAB)
Plug 'vim-airline/vim-airline'

" Directories tree configuration
Plug 'scrooloose/nerdtree'

" Dev icons 
" Plug 'ryanoasis/vim-devicons'

" Auto pairs 
Plug 'jiangmiao/auto-pairs'

" Grammar check for English
" Plug 'rhysd/vim-grammarous'

"Goyo for Zen Mode 
Plug 'junegunn/goyo.vim'

" Interactive jupyter-notebook
Plug 'jupyter-vim/jupyter-vim'

" Markdown snippets 
Plug 'SirVer/ultisnips'
Plug 'honza/vim-snippets'
" tabular plugin is used to format tables
Plug 'godlygeek/tabular'
" JSON front matter highlight plugin
Plug 'elzr/vim-json'
Plug 'plasticboy/vim-markdown'
"Plug 'vim-pandoc/vim-pandoc-syntax'

" Markdown preview
Plug 'iamcco/markdown-preview.nvim', { 'do': 'cd app && yarn install' }

call plug#end()

" GRUVBOX Configuration
set background=dark
let g:gruvbox_material_background='medium'
colorscheme gruvbox-material

" Easy motion Configuran

let mapleader=" "
nmap s <Plug>(easymotion-s2)
nmap t <Plug>(easymotion-t2)


" LSP configuration 

lua<< EOF
require'lspconfig'.pyright.setup{on_attach=require'completion'.on_attach}
EOF

" Airline configuration
let g:airline#extensions#tabline#enabled = 1


" Nerd tree - directorie configuration 
let NERDTreeQuitOnOpen= 1
nnoremap <silent> <F2> :NERDTreeFind<CR>
nnoremap <silent> <F3> :NERDTreeToggle<CR>

" Jupyter Qtconsole configuration
" Run current file
nnoremap <buffer> <silent> <localleader>R :JupyterRunFile<CR>
nnoremap <buffer> <silent> <localleader>I :PythonImportThisFile<CR>

" Change to directory of current file
nnoremap <buffer> <silent> <localleader>d :JupyterCd %:p:h<CR>

" Send a selection of lines
nnoremap <buffer> <silent> <localleader>X :JupyterSendCell<CR>
nnoremap <buffer> <silent> <localleader>E :JupyterSendRange<CR>
nmap     <buffer> <silent> <localleader>e <Plug>JupyterRunTextObj
vmap     <buffer> <silent> <localleader>e <Plug>JupyterRunVisual

" Debugging maps
nnoremap <buffer> <silent> <localleader>b :PythonSetBreak<CR>
"------------------------------
" Markdown Configuration begins
" -----------------------------
" URL https://jdhao.github.io/2019/01/15/markdown_edit_preview_nvim/ 
" Do not use <tab> if you use https://github.com/Valloric/YouCompleteMe.
let g:UltiSnipsExpandTrigger="<tab>"  " use <Tab> to trigger autocompletion
let g:UltiSnipsJumpForwardTrigger="<c-j>"
let g:UltiSnipsJumpBackwardTrigger="<c-k>"

" disable header folding
let g:vim_markdown_folding_disabled = 1

" do not use conceal feature, the implementation is not so good
"Markdown conceal configurations
"URL: https://github.com/preservim/vim-markdown#options
let g:vim_markdown_conceal = 0
let g:tex_conceal = ""
let g:vim_markdown_math = 1
let g:vim_markdown_conceal_code_blocks = 0

" support front matter of various format
let g:vim_markdown_frontmatter = 1  " for YAML format
let g:vim_markdown_toml_frontmatter = 1  " for TOML format
let g:vim_markdown_json_frontmatter = 1  " for JSON format

" Pandoc syntax  configuration
"augroup pandoc_syntax
"    au! BufNewFile,BufFilePre,BufRead *.md set filetype=markdown.pandoc
"augroup END


"Markdown preview 
"URL: https://github.com/iamcco/markdown-preview.nvim

" do not close the preview tab when switching to other buffers
let g:mkdp_auto_close = 0

nnoremap <M-m> :MarkdownPreview<CR>

"--------------------------
"Markdown configuration ends
"---------------------------


"------------------------
" COC configuration begin
"------------------------
" Set internal encoding of vim, not needed on neovim, since coc.nvim using some
" unicode characters in the file autoload/float.vim
" :wset encoding=utf-8

" TextEdit might fail if hidden is not set.
set hidden

" Some servers have issues with backup files, see #649.
set nobackup
set nowritebackup

" Give more space for displaying messages.
set cmdheight=2

" Having longer updatetime (default is 4000 ms = 4 s) leads to noticeable
" delays and poor user experience.
set updatetime=300

" Don't pass messages to |ins-completion-menu|.
set shortmess+=c

" Always show the signcolumn, otherwise it would shift the text each time
" diagnostics appear/become resolved.
if has("nvim-0.5.0") || has("patch-8.1.1564")
  " Recently vim can merge signcolumn and number column into one
  set signcolumn=number
else
  set signcolumn=yes
endif

" Use tab for trigger completion with characters ahead and navigate.
" NOTE: Use command ':verbose imap <tab>' to make sure tab is not mapped by
" other plugin before putting this into your config.
inoremap <silent><expr> <TAB>
      \ pumvisible() ? "\<C-n>" :
      \ CheckBackspace() ? "\<TAB>" :
      \ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

function! CheckBackspace() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <c-space> to trigger completion.
if has('nvim')
  inoremap <silent><expr> <c-space> coc#refresh()
else
  inoremap <silent><expr> <c-@> coc#refresh()
endif

" Make <CR> auto-select the first completion item and notify coc.nvim to
" format on enter, <cr> could be remapped by other vim plugin
inoremap <silent><expr> <cr> pumvisible() ? coc#_select_confirm()
                              \: "\<C-g>u\<CR>\<c-r>=coc#on_enter()\<CR>"

" Use `[g` and `]g` to navigate diagnostics
" Use `:CocDiagnostics` to get all diagnostics of current buffer in location list.
nmap <silent> [g <Plug>(coc-diagnostic-prev)
nmap <silent> ]g <Plug>(coc-diagnostic-next)

" GoTo code navigation.
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

" Use K to show documentation in preview window.
nnoremap <silent> K :call ShowDocumentation()<CR>

function! ShowDocumentation()
  if CocAction('hasProvider', 'hover')
    call CocActionAsync('doHover')
  else
    call feedkeys('K', 'in')
  endif
endfunction

" Highlight the symbol and its references when holding the cursor.
autocmd CursorHold * silent call CocActionAsync('highlight')

" Symbol renaming.
nmap <leader>rn <Plug>(coc-rename)

" Formatting selected code.
xmap <leader>f  <Plug>(coc-format-selected)
nmap <leader>f  <Plug>(coc-format-selected)

augroup mygroup
  autocmd!
  " Setup formatexpr specified filetype(s).
  autocmd FileType typescript,json setl formatexpr=CocAction('formatSelected')
  " Update signature help on jump placeholder.
  autocmd User CocJumpPlaceholder call CocActionAsync('showSignatureHelp')
augroup end

" Applying codeAction to the selected region.
" Example: `<leader>aap` for current paragraph
xmap <leader>a  <Plug>(coc-codeaction-selected)
nmap <leader>a  <Plug>(coc-codeaction-selected)

" Remap keys for applying codeAction to the current buffer.
nmap <leader>ac  <Plug>(coc-codeaction)
" Apply AutoFix to problem on the current line.
nmap <leader>qf  <Plug>(coc-fix-current)

" Run the Code Lens action on the current line.
nmap <leader>cl  <Plug>(coc-codelens-action)

" Map function and class text objects
" NOTE: Requires 'textDocument.documentSymbol' support from the language server.
xmap if <Plug>(coc-funcobj-i)
omap if <Plug>(coc-funcobj-i)
xmap af <Plug>(coc-funcobj-a)
omap af <Plug>(coc-funcobj-a)
xmap ic <Plug>(coc-classobj-i)
omap ic <Plug>(coc-classobj-i)
xmap ac <Plug>(coc-classobj-a)
omap ac <Plug>(coc-classobj-a)

" Remap <C-f> and <C-b> for scroll float windows/popups.
if has('nvim-0.4.0') || has('patch-8.2.0750')
  nnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  nnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
  inoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? "\<c-r>=coc#float#scroll(1)\<cr>" : "\<Right>"
  inoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? "\<c-r>=coc#float#scroll(0)\<cr>" : "\<Left>"
  vnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  vnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
endif

" Use CTRL-S for selections ranges.
" Requires 'textDocument/selectionRange' support of language server.
nmap <silent> <C-s> <Plug>(coc-range-select)
xmap <silent> <C-s> <Plug>(coc-range-select)

" Add `:Format` command to format current buffer.
command! -nargs=0 Format :call CocActionAsync('format')

" Add `:Fold` command to fold current buffer.
command! -nargs=? Fold :call     CocAction('fold', <f-args>)

" Add `:OR` command for organize imports of the current buffer.
command! -nargs=0 OR   :call     CocActionAsync('runCommand', 'editor.action.organizeImport')

" Add (Neo)Vim's native statusline support.
" NOTE: Please see `:h coc-status` for integrations with external plugins that
" provide custom statusline: lightline.vim, vim-airline.
set statusline^=%{coc#status()}%{get(b:,'coc_current_function','')}

" Mappings for CoCList
" Show all diagnostics.
nnoremap <silent><nowait> <space>a  :<C-u>CocList diagnostics<cr>
" Manage extensions.
nnoremap <silent><nowait> <space>e  :<C-u>CocList extensions<cr>
" Show commands.
nnoremap <silent><nowait> <space>c  :<C-u>CocList commands<cr>
" Find symbol of current document.
nnoremap <silent><nowait> <space>o  :<C-u>CocList outline<cr>
" Search workspace symbols.
nnoremap <silent><nowait> <space>s  :<C-u>CocList -I symbols<cr>
" Do default action for next item.
nnoremap <silent><nowait> <space>j  :<C-u>CocNext<CR>
" Do default action for previous item.
nnoremap <silent><nowait> <space>k  :<C-u>CocPrev<CR>
" Resume latest coc list.
nnoremap <silent><nowait> <space>p  :<C-u>CocListResume<CR>

"----------------------
" COC configuration end
"----------------------
"

```

