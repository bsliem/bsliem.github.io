# =========================================================
# .Rprofile — bsliem.github.io
# Quarto website / RStudio / GitHub Pages
# =========================================================

options(
  repos = c(CRAN = "https://cloud.r-project.org"),
  encoding = "UTF-8",
  scipen = 999,
  max.print = 1000,
  width = 120
)

.project_name <- "bsliem.github.io"
.project_url  <- "https://bsliem.github.io/"

# ==== BASIC HELPERS ====

norm_path <- function(path = ".") {
  normalizePath(path, winslash = "/", mustWork = FALSE)
}

proj_root <- function(path = getwd()) {
  path <- norm_path(path)
  
  repeat {
    if (file.exists(file.path(path, "_quarto.yml"))) return(path)
    
    parent <- dirname(path)
    if (identical(parent, path)) break
    path <- parent
  }
  
  norm_path(getwd())
}

pj <- function() {
  p <- proj_root()
  setwd(p)
  cat("📁 Project:", p, "\n")
  invisible(p)
}

wd <- function() {
  out <- norm_path(getwd())
  cat("📁 Working directory:", out, "\n")
  invisible(out)
}

open_file <- function(path = ".") {
  path <- norm_path(path)
  
  if (!file.exists(path) && !dir.exists(path)) {
    cat("❌ Không tồn tại:", path, "\n")
    return(invisible(NULL))
  }
  
  sys <- Sys.info()[["sysname"]]
  
  if (sys == "Windows") {
    shell.exec(path)
  } else if (sys == "Darwin") {
    system2("open", path)
  } else {
    system2("xdg-open", path)
  }
  
  invisible(path)
}

# ==== QUARTO WEBSITE ====

qr <- function() {
  pj()
  cat("🚀 quarto render\n")
  status <- system2("quarto", "render")
  
  if (identical(status, 0L)) {
    cat("✅ Render xong: docs/index.html\n")
  } else {
    cat("⚠️ Render có lỗi, xem thông báo phía trên.\n")
  }
  
  invisible(status)
}

qp <- function() {
  pj()
  cat("👀 quarto preview\n")
  cat("Nhấn Ctrl + C để dừng preview.\n\n")
  system2("quarto", "preview")
}

qclean <- function() {
  pj()
  
  if (dir.exists("docs")) {
    unlink("docs", recursive = TRUE, force = TRUE)
    cat("🧹 Đã xóa thư mục docs/\n")
  }
  
  qr()
}

open_site <- function() {
  browseURL(.project_url)
  invisible(.project_url)
}

odocs <- function() {
  open_file(file.path(proj_root(), "docs"))
}

oindex <- function() {
  open_file(file.path(proj_root(), "index.qmd"))
}

ostyles <- function() {
  open_file(file.path(proj_root(), "styles.css"))
}

oyml <- function() {
  open_file(file.path(proj_root(), "_quarto.yml"))
}

oposts <- function() {
  open_file(file.path(proj_root(), "posts"))
}

# ==== GIT ====

get_git_branch <- function() {
  tryCatch({
    b <- system2("git", c("branch", "--show-current"), stdout = TRUE, stderr = FALSE)
    if (length(b) == 0 || !nzchar(trimws(b[1]))) return("NA")
    trimws(b[1])
  }, error = function(e) "NA")
}

gs <- function() {
  pj()
  system("git status")
  invisible(NULL)
}

gl <- function(n = 10) {
  pj()
  n <- as.integer(n)
  if (is.na(n) || n < 1) n <- 10
  
  system2(
    "git",
    c("log", "--oneline", "--graph", "--decorate", "-n", n)
  )
  
  invisible(NULL)
}

gpull <- function() {
  pj()
  system("git pull --rebase")
  invisible(NULL)
}

gp <- function(msg = "update website", render_first = TRUE) {
  pj()
  
  if (requireNamespace("rstudioapi", quietly = TRUE)) {
    try(rstudioapi::executeCommand("saveAllSourceDocs"), silent = TRUE)
  }
  
  if (isTRUE(render_first)) {
    qr()
  }
  
  msg <- trimws(msg)
  if (!nzchar(msg)) msg <- "update website"
  
  full_msg <- paste0(
    format(Sys.time(), "%Y-%m-%d %H:%M"),
    " | ",
    get_git_branch(),
    " | ",
    msg
  )
  
  system("git add -A")
  
  changed <- system("git diff --cached --quiet")
  
  if (identical(changed, 0L)) {
    cat("📭 Không có thay đổi để commit.\n")
    return(invisible(NULL))
  }
  
  commit_status <- system(paste("git commit -m", shQuote(full_msg)))
  
  if (!identical(commit_status, 0L)) {
    cat("⚠️ Commit lỗi.\n")
    return(invisible(NULL))
  }
  
  push_status <- system("git push")
  
  if (identical(push_status, 0L)) {
    cat("🚀 Đã push:", full_msg, "\n")
  } else {
    cat("⚠️ Commit xong nhưng push lỗi.\n")
  }
  
  invisible(full_msg)
}

# Alias ngắn
s <- gp

# ==== FILES ====

lsd <- function(path = ".") {
  x <- list.files(path, full.names = TRUE, no.. = TRUE)
  
  if (length(x) == 0) {
    cat("📭 Không có file/thư mục.\n")
    return(invisible(NULL))
  }
  
  info <- file.info(x)
  
  df <- data.frame(
    type = ifelse(info$isdir, "📁", "📄"),
    name = basename(x),
    modified = format(info$mtime, "%Y-%m-%d %H:%M"),
    stringsAsFactors = FALSE
  )
  
  print(df, row.names = FALSE)
  invisible(df)
}

ff <- function(pattern, path = ".") {
  x <- list.files(path, pattern = pattern, recursive = TRUE, full.names = TRUE, ignore.case = TRUE)
  
  if (length(x) == 0) {
    cat("❌ Không tìm thấy:", pattern, "\n")
    return(invisible(NULL))
  }
  
  print(x)
  invisible(x)
}

recent <- function(path = ".", n = 10) {
  x <- list.files(path, recursive = TRUE, full.names = TRUE, no.. = TRUE)
  
  if (length(x) == 0) {
    cat("📭 Không có file.\n")
    return(invisible(NULL))
  }
  
  info <- file.info(x)
  ord <- order(info$mtime, decreasing = TRUE)
  x <- x[ord][seq_len(min(n, length(x)))]
  info <- file.info(x)
  
  df <- data.frame(
    file = x,
    modified = format(info$mtime, "%Y-%m-%d %H:%M"),
    stringsAsFactors = FALSE
  )
  
  print(df, row.names = FALSE)
  invisible(df)
}

# ==== STARTUP MENU ====

if (interactive()) {
  cat("\n")
  cat("🌿 ", .project_name, "\n", sep = "")
  cat("🌐 ", .project_url, "\n", sep = "")
  cat("🌱 Branch: ", get_git_branch(), "\n\n", sep = "")
  
  cat("Quarto ####\n")
  cat("  qr()              quarto render\n")
  cat("  qp()              quarto preview\n")
  cat("  qclean()          xóa docs/ rồi render lại\n")
  cat("  open_site()       mở website online\n\n")
  
  cat("Open ####\n")
  cat("  oindex()          mở index.qmd\n")
  cat("  ostyles()         mở styles.css\n")
  cat("  oyml()            mở _quarto.yml\n")
  cat("  oposts()          mở thư mục posts/\n")
  cat("  odocs()           mở thư mục docs/\n\n")
  
  cat("Git ####\n")
  cat("  gs()              git status\n")
  cat("  gl()              git log\n")
  cat("  gpull()           git pull --rebase\n")
  cat("  gp('message')     render + add + commit + push\n")
  cat("  s('message')      alias của gp()\n\n")
  
  cat("Files ####\n")
  cat("  lsd()             xem file/thư mục\n")
  cat("  recent()          xem file mới sửa gần đây\n")
  cat("  ff('keyword')     tìm file\n\n")
}
